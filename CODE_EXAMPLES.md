# 代码示例与开源项目

> 基于 VLA-Handbook 社区笔记和开源项目整理
> 最后更新: 2026-03-30

---

## 1. 开源 VLA 训练栈

### UnifolM-VLA-0（⭐ 推荐）

**链接**: `theory/unifolm_vla_0_unitree_2026.md`

**特点**: 
- 专为宇树机器人设计的开源训练栈
- 完整的数据处理、训练、推理 pipeline
- 适合想跑通全流程的开发者

**关键资源**:
- GitHub: 搜索 UnifolM
- 配套文档: `theory/unifolm_vla_0_unitree_2026.md`

---

### StarVLA（模块化 LEGO-like）

**链接**: `theory/starvla_lego_like_vla_codebase_2026.md`

**特点**:
- LEGO-like 模块化架构
- 可拆卸的 Vision Encoder / LLM Backbone / Action Head
- 适合研究架构选择和组件替换

---

### π0 系列（Physical Intelligence）

**模型权重**: Open Weights available

| 版本 | 链接 | 特点 |
|------|------|------|
| π0 | Open Weights | 基础 VLA 模型 |
| π0.5 | `theory/pi0_5_dissection.md` | 分层推理 + 开放世界泛化 |
| π0.6 | `theory/pi0_6_dissection.md` | RL + Recap + Action Expert |
| π*0.6 (Pi-Star) | `theory/pi0_6_dissection.md` | 自我改进，真机持续学习 |

**代码分析**: `theory/pi0_code_analysis.md`

---

## 2. Diffusion Policy 实现

### 核心参考

| 资源 | 链接 |
|------|------|
| Diffusion Policy 理论 | `theory/diffusion_policy.md` |
| Flow Matching 原理 | `theory/pi0_flow_matching.md` |
| π0 代码分析 | `theory/pi0_code_analysis.md` |

### 关键代码模式

```python
# Flow Matching 推理（简化版）
# 核心: 从噪声直接预测目标动作，5-20步达到50Hz

def flow_matching_step(x_t, t, model):
    """
    x_t: 当前状态（含噪声的动作）
    t: 时间步 [0, 1]
    model: VLA模型
    """
    # 预测从 x_t 到目标动作的速度向量
    velocity = model(x_t, t)
    
    # 积分得到目标动作
    x_1 = x_t + velocity * dt
    return x_1

# 5-20步完成推理（vs Diffusion需要50+步）
```

---

## 3. Action Tokenization

### 离散 Token（RT-1/2 风格）

```python
# 动作空间离散化
action_dim = 7  # x, y, z, roll, pitch, yaw, gripper
num_bins = 256  # 每个维度256个桶

def discretize_action(action, bins_per_dim=256):
    """连续动作 -> 离散Token"""
    tokens = []
    for a in action:
        bin_idx = int((a - min_val) / (max_val - min_val) * (bins_per_dim - 1))
        bin_idx = clip(bin_idx, 0, bins_per_dim - 1)
        tokens.append(bin_idx)
    return tokens  # 返回离散token序列

def detokenize_action(tokens, bins_per_dim=256):
    """离散Token -> 连续动作"""
    actions = []
    for t in tokens:
        a = min_val + (t / (bins_per_dim - 1)) * (max_val - min_val)
        actions.append(a)
    return actions
```

### Flow Matching Action

```python
# π0 采用的方式：预测velocity
def compute_flow_matching_loss(pred_action, target_action, timesteps):
    """
    预测从当前动作到目标动作的velocity
    比直接回归更稳定，比Diffusion更快
    """
    velocity = target_action - current_action
    pred_velocity = model(obs, current_action, timesteps)
    return MSE(pred_velocity, velocity)
```

---

## 4. 多模态融合代码模式

```python
# VLA 标准融合架构
class VLAProcessor:
    def __init__(self, vision_encoder, language_encoder, backbone, action_head):
        self.vision_encoder = vision_encoder      # ViT / DINOv2 / SigLIP
        self.language_encoder = language_encoder  # LLM / BERT
        self.backbone = backbone                  # Transformer
        self.action_head = action_head            # Token / Diffusion / Flow

    def forward(self, image, language_instruction, proprio):
        # 1. 视觉编码
        vision_tokens = self.vision_encoder(image)  # [B, N_v, D]
        
        # 2. 语言编码
        text_tokens = self.language_encoder(language_instruction)  # [B, N_t, D]
        
        # 3. 位置编码（可能是robot proprio）
        if proprio is not None:
            proprio_tokens = self.proprio_encoder(proprio)  # [B, N_p, D]
            tokens = concat([vision_tokens, text_tokens, proprio_tokens])
        else:
            tokens = concat([vision_tokens, text_tokens])
        
        # 4. Transformer backbone
        features = self.backbone(tokens)
        
        # 5. Action head
        action = self.action_head(features)
        return action
```

---

## 5. Sim2Real 关键代码

### Domain Randomization

```python
# Sim2Real: Domain Randomization 要点
# 来自社区实战笔记（deployment/community_field_notes_github.md）

def randomize_sim_params():
    """
    关键随机化维度（来自GitHub Issues经验）：
    1. 物体纹理/颜色
    2. 光照条件
    3. 相机位姿
    4. 物理参数（摩擦力、质量）
    """
    randomization_config = {
        'texture': random.choice(textures),
        'lighting': random.uniform(0.5, 1.5),  # 光照强度
        'camera_pos_noise': np.random.normal(0, 0.02),  # 相机位置噪声
        'friction': random.uniform(0.3, 1.2),   # 摩擦系数
        'mass_scale': random.uniform(0.8, 1.2),  # 质量缩放
    }
    return randomization_config
```

### 动作空间对齐

```python
# ACT 实战要点（来自社区笔记）
# ACT: 50 episodes就能work，不需要大数据量

# 关键超参
act_config = {
    'policy_lr': 1e-5,
    'num_queries': 16,         # action chunk长度
    'kl_weight': 10,           # KL散度权重
    'hidden_dim': 512,
    'batch_size': 8,
    'num_epochs': 100,
}

# 注意：ACT对动作空间对齐非常敏感
# Sim2Real失败往往不是算法问题，而是物理参数没校准
```

---

## 6. LeRobot 实战

**GitHub**: `https://github.com/huggingface/lerobot`

**关键经验**（来自 community_field_notes_english.md）:
- LeRobot 是当前最活跃的开源机器人代码库
- 支持多种机器人形态
- HF Dataset 直接对接

```bash
# LeRobot 快速上手
pip install lerobot
lerobot record --robot-type so100
```

---

## 7. GPU 兼容矩阵（来自 GitHub Issues）

**来源**: `deployment/community_field_notes_github.md`

| GPU 系列 | 兼容性 | 备注 |
|---------|-------|------|
| RTX 4090 | ✅ 完全支持 | 推荐开发卡 |
| RTX 3090 | ✅ 支持 | 训练 OK |
| RTX 50 系列 | ⚠️ 部分支持 | 需检查 CUDA 版本 |
| Jetson | ⚠️ 边缘部署 | 需要量化 (QLoRA) |
| A100/H100 | ✅ 完全支持 | 服务器训练 |

---

## 8. 关键文件路径

| 资源 | 路径 |
|------|------|
| 自动化 Pipeline | `scripts/SCRIPTS.md` |
| LeRobot | HuggingFace/lerobot |
| Isaac Lab | `theory/isaac_lab.md` |
| Loss Functions | `theory/loss_functions_snippets.py` |
| 数学公式速查 | `theory/ascii_cheatsheet.md` |
