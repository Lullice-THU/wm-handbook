# VLA 核心架构：从 RT-1 到 π0 的演进

> 整理自: [VLA-Handbook - vla_arch.md](https://github.com/sou350121/VLA-Handbook/blob/main/theory/vla_arch.md)

---

## 1. VLA 通用架构模板

```
┌─────────────────────────────────────────────────────────────┐
│                    VLA 通用架构模板                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   📷 Image          📝 Language                             │
│       │                  │                                  │
│       ▼                  ▼                                  │
│   ┌──────────┐    ┌────────────┐                           │
│   │  Vision  │    │  Language  │                           │
│   │  Encoder │    │  Encoder   │                           │
│   │ (ViT/CNN)│    │(LLM/BERT)  │                           │
│   └────┬─────┘    └──────┬─────┘                           │
│        │                 │                                  │
│        └────────┬────────┘                                  │
│                 │ Fusion                                    │
│                 ▼                                          │
│        ┌──────────────────┐                                 │
│        │   Transformer    │                                 │
│        │     Backbone     │                                 │
│        └────────┬─────────┘                                 │
│                 │                                          │
│                 ▼                                          │
│        ┌──────────────────┐                                 │
│        │   Action Head    │                                 │
│        │ Token/Diff/Flow  │                                 │
│        └────────┬─────────┘                                 │
│                 │                                          │
│                 ▼                                          │
│         🦾 Robot Action                                     │
└─────────────────────────────────────────────────────────────┘
```

**核心演进路线:**
```
RT-1 (2022) → RT-2 (2023) → π0 (2024) → π0.6 (2025) → π*0.6 (2025)
  小模型       大VLM        高效推理     RL强化       动作专家
  机器人数据   +互联网数据   +精细控制    +Recap       +自我改进
```

---

## 2. RT-1 (Robotics Transformer 1) — 2022

### 核心思想
将机器人控制建模为 **Token 生成问题**，使用 Transformer 处理多模态输入。

### 架构
- EfficientNet (Vision) + FiLM (Language conditioning) + TokenLearner + Transformer

### Action Tokenization
- 将连续动作空间 (x, y, z, roll, pitch, yaw, gripper) **离散化为 256 个 bins**
- 输出是离散 Token 序列，代表动作维度

### 关键设计: TokenLearner
- 显著减少视觉 Token 数量：81 → 8
- 提高推理速度

### 数据规模
- 130k episodes（17个月数据）

### 局限性
- 泛化能力有限
- 主要依赖大规模收集的机器人数据
- 缺乏互联网知识迁移能力

---

## 3. RT-2 (Robotics Transformer 2) — 2023

### 核心思想
**VLA = VLM + Action Tokens**
直接微调预训练的 VLM（如 PaLI-X, PaLM-E）用于机器人控制。

### 架构
- 基于大规模 VLM (Vision-Language Model) 微调

### Co-fine-tuning
- **混合训练**：互联网 VQA 数据 + 机器人操作数据
- 机器人动作被表示为特殊的**文本 Token**（如 "1 128 90 ..."）
- 与自然语言 Token 共享词表

### 涌现能力 (Emergent Capabilities)
- 能够理解未见过的指令
- 例: "pick up the extinct animal" → 抓恐龙玩具
- 得益于 VLM 的语义理解能力

### 支持 Chain-of-Thought
- 简单推理步骤

### 局限性
- 推理速度慢（大模型）
- 难以在边缘端实时运行
- 闭源

---

## 4. OpenVLA / Octo — 开源 VLA

### Octo
- **架构**: 基于 Diffusion Policy 的 Transformer 架构
- **特点**: 支持多种观察空间（Proprioception, Images）和动作空间
- **训练**: 在 Open X-Embodiment (OXE) 数据集上训练

### OpenVLA
- **架构**: Llama 2 (7B) + DINOv2 / SigLIP (Vision Encoder)
- **Action Head**: 
  - 并没有直接输出文本 Token
  - 使用专门的 Action Head（Linear Layer）预测去离散化的动作 Token
  - Action Detokenization 还原为连续动作
- **优化**: 支持 4-bit 量化（QLoRA）训练和推理，适合消费级显卡

---

## 5. Physical Intelligence (π) 系列

### 5.1 π0 (Pi-Zero) — 2024

**定位**: 通用 VLA 基础模型，强调跨形态（Cross-Embodiment）和物理世界理解

**架构特点**:
- 类似 RT 系列，但更强调对物理动力学的理解
- 可能采用更高效的 Action Tokenizer 以适应高频控制

**数据**: 混合多种机器人数据（Arms, Quadrupeds, Humanoids）

**状态**: 已开源（Open Weights）

---

### 5.2 π0.5 (Pi-Zero-Point-Five) — April 2025

**核心升级**: 
- **开放世界泛化** (Open-world Generalization)
- **分层推理** (Hierarchical Inference)

**架构特点**:
- **统一模型**: 同时负责高层语义规划（Subtask Prediction）和底层电机控制（Motor Control）
- 模型"自言自语"下一步要做什么，然后执行

- **异构数据训练**: 大量互联网视频（YouTube）+ 模拟数据，通过 Co-training 实现新环境适应

- **混合架构**: 
  - 预训练阶段可能使用离散 Token（FAST tokenizer）提高效率
  - 推理阶段使用 Flow Matching 生成连续动作

**深度解析**: `theory/pi0_5_dissection.md`

---

### 5.3 π0.6 & π*0.6 (Pi-Star) — November 2025

**核心升级**: **RL 强化** + **Recap 算法**

**Backbone**: 升级为 5B Parameter VLM，增强对复杂指令和环境的理解

**π*0.6 (Pi-Star) 关键算法 - Recap**:
- 一种 **Offline RL** 方法
- 模型通过"复盘"过去成功与失败经验进行自我提升
- 不仅仅模仿（BC），还能反思

**性能飞跃**:
- 长序列任务（折叠衣物、组装纸箱）：吞吐量翻倍，失败率降低 2x
- **Self-Improvement**: 具备在真机运行中持续学习的能力

**Action Expert**:
- 引入专门的动作专家模块
- 专门处理精细操作
- 解决大语言模型在精细运动控制上的"手笨"问题

**深度解析**: `theory/pi0_6_dissection.md`

---

## 6. 模型对比总结

| 模型 | 基础架构 | Action 输出 | 训练数据 | 优势 | 劣势 |
|------|---------|------------|---------|------|------|
| RT-1 | EfficientNet + Transformer | Discrete Tokens | Robot Data Only | 推理快，稳定性高 | 泛化差，无语义推理 |
| RT-2 | PaLI-X / PaLM-E | Text Tokens | Web + Robot Data | 语义理解强，Zero-shot | 推理慢，闭源 |
| OpenVLA | Llama 2 + SigLIP | Action Head | OXE Dataset | 开源，支持量化，易部署 | 性能略逊闭源 SOTA |
| WALL-OSS | Qwen2.5 VLMoE | Dual Branches (Flow + FAST) | Cross-Embodiment | COT 推理，双分支，已开源 | 训练资源需求高 |
| π0.6 | Gemma 3 + Action Expert | Specialized | Cross-Embodiment + RL | 泛化强，精细操作好，已开源 | 训练极其昂贵 |

---

## 7. 动作生成三范式

> 详见: `theory/action_representations.md`

```
┌─────────────────────────────────────────────────────────────┐
│               动作生成范式对比                               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ① 离散 Token（RT-1/2）                                     │
│     优点: 训练简单，推理快                                   │
│     缺点: 精度粗糙，多模态分布处理能力有限                   │
│                                                             │
│  ② Diffusion（扩散模型）                                    │
│     优点: 精度高，可处理多模态动作分布                      │
│     缺点: 推理慢（50+ steps），难以实时控制                 │
│                                                             │
│  ③ Flow Matching（π0 系列采用）⭐                          │
│     优点: 精度高 + 推理快（5-20 步达到 50Hz）               │
│     缺点: 实现复杂度高                                      │
│                                                             │
│  核心原因: Flow Matching 的 ODE 直线路径 vs Diffusion 的曲线│
│  去噪，5-20 步推理实现 50Hz 控制                            │
└─────────────────────────────────────────────────────────────┘
```

详见: `theory/pi0_flow_matching.md` — Flow Matching 原理拆解

---

## 8. 面试高频考点

### Q1: Action Tokenization — 为什么要离散化？连续回归有什么问题？
- **答**: 多模态分布处理能力
- 连续回归难以处理多峰分布（同一个指令对应多种正确动作）
- 离散化让模型学习"动作的分布"

### Q2: Co-fine-tuning — 为什么要混合互联网数据？
- **答**: 保持 VLM 的语义能力，防止灾难性遗忘
- 如果只用机器人数据微调，VLM 的语义理解能力会退化

### Q3: Sim-to-Real — OpenVLA 如何在真机上部署？
- **答**: 量化，VLM 蒸馏
- QLoRA 4-bit 量化 + Action Head 蒸馏

### Q4: Flow Matching vs Diffusion
- **答**: 
  - Diffusion: 曲线去噪路径，需要 50+ 步
  - Flow Matching: ODE 直线路径，5-20 步
  - 关键优势: 推理速度 5-10x 提升，同时精度不下降

---

## 9. 前沿扩展: Figure Helix

**论文**: Figure Helix 0.2: Full-Body Autonomy

**架构**: S1 + S2 双系统人形 VLA

**链接**: `theory/frontier/figure_helix_02_full_body_autonomy_2026.md`

---

## 10. 相关链接

| 资源 | 链接 |
|------|------|
| VLA 架构总览 | `theory/vla_arch.md` |
| 动作生成三范式 | `theory/action_representations.md` |
| Flow Matching 原理 | `theory/pi0_flow_matching.md` |
| π0.5 深度解析 | `theory/pi0_5_dissection.md` |
| π0.6 深度解析 | `theory/pi0_6_dissection.md` |
| π0 代码分析 | `theory/pi0_code_analysis.md` |
| VLA 研究主线 | `theory/vla_research_mainline.md` |
| Diffusion Policy | `theory/diffusion_policy.md` |
