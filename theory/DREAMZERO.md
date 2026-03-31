# DreamZero: World Action Models Are Zero-Shot Policies — 深度解析

> **论文**: [arXiv:2401.04483](https://arxiv.org/abs/2401.04483)
> **核心问题**: World Model 能否不训练直接生成 zero-shot policy？
> **关键词**: World Action Model, Zero-Shot, Video Prediction, Robotic Manipulation

---

## 一句话总结

DreamZero 证明了 **World Model 可以直接作为 Action Model 使用**，无需在特定任务上微调即可生成有效的机器人策略——这重新定义了 world model 在机器人控制中的角色。

---

## 核心贡献

### 1. 角色重新定义

传统观点：
```
World Model = 预测未来的视频生成器
Action Model = 输出动作的控制器
```

DreamZero 的观点：
```
World Model = 联合预测 video + action 的统一模型（World Action Model）
```

**关键洞察**：如果 world model 能预测"未来视频"，它就能同时预测"应该采取的动作"。

### 2. Zero-Shot Policy 能力

**定义**：无需在目标机器人/任务上训练，直接生成策略。

**实现方式**：
1. 预训练一个 world model（在大规模视频数据上）
2. 推理时，给定当前 observation + goal
3. world model rollouts：在想象中"预测"多个候选动作序列的未来
4. 选择预期奖励最高的动作序列

### 3. 联合建模框架

```
Loss = λ₁·L_video + λ₂·L_action + λ₃·L_consistency
       ├── L_video: 视频重建损失
       ├── L_action: 动作预测损失
       └── L_consistency: 视频-动作一致性损失
```

---

## 技术细节

### 架构

| 组件 | 设计 |
|------|------|
| Backbone | Diffusion Transformer (DiT) |
| 视频建模 | 预测未来 16 帧 |
| 动作建模 | 离散动作 token 预测 |
| 条件 | text goal + 当前 frame |

### 关键超参

| 参数 | 值 | 说明 |
|------|-----|------|
| 视频预测长度 | 16 帧 | 约 0.5 秒 @ 30fps |
| 动作 chunk 长度 | 8 步 | 约 0.25 秒 @ 30Hz |
| rollout 候选数 | 16 | MC sampling |
| 推理频率 | 10 Hz | 100ms/决策 |

### 数据规模

- 预训练：800K 机器人 episode（多个机器人形态）
- 评估：8 个未见过的任务

---

## 实验结果

### Zero-Shot 任务迁移

| 任务 | 成功率 | 基线对比 |
|------|---------|---------|
| 抓取未知物体 | 72% | SOTA: 68% |
| 开门 | 65% | SOTA: 71% |
| 物体重排列 | 58% | SOTA: 52% |
| 抽屉开关 | 70% | SOTA: 75% |
| 平均 | **66%** | SOTA: **66%** |

**结论**：DreamZero 在 zero-shot 设定下与全量训练的 SOTA 持平。

### 消融实验

| 组件 | 贡献 |
|------|------|
| 联合建模 | +8% 成功率 |
| 想象力 rollout | +12% 成功率 |
| 动作一致性损失 | +5% 成功率 |

---

## 工程实现

### 推理 pipeline

```python
def dreamzero_policy(observation, goal, world_model):
    # 1. 编码当前状态
    obs_enc = encode(observation)
    goal_enc = encode(goal)
    
    # 2. 生成候选动作序列
    candidates = []
    for _ in range(16):  # 16 个 MC samples
        action_seq = world_model.sample_action(
            obs_enc, goal_enc, T=8
        )
        candidates.append(action_seq)
    
    # 3. 在想象中 rollout
    rewards = []
    for action_seq in candidates:
        imagined_future = world_model.imagine(
            obs_enc, action_seq, goal_enc
        )
        reward = world_model.predict_reward(imagined_future)
        rewards.append(reward)
    
    # 4. 选择最佳动作序列
    best_idx = argmax(rewards)
    return candidates[best_idx][0]  # 返回第一个动作
```

### 与 VLA 的区别

| 维度 | VLA (RT-2/π0) | DreamZero |
|------|--------------|-----------|
| 训练方式 | 监督微调 | 预训练 + 推理时规划 |
| 动作生成 | 直接输出 | imagination + selection |
| zero-shot | ❌ 需要微调 | ✅ 原生支持 |
| 推理速度 | 50Hz | 10Hz（慢 5×） |

---

## 局限性

1. **推理速度慢**：imagination rollout 需要多次 forward，10Hz vs VLA 的 50Hz
2. **候选数量受限**：16 个 MC samples 可能不够覆盖复杂任务
3. **视频预测质量**：想象的质量直接影响策略选择
4. **长 horizon 任务**：16 帧预测窗口可能不够

---

## 与其他工作的关系

### 相关论文

| 论文 | 关系 |
|------|------|
| WorldEval | DreamZero 是 WorldEval "更强终点"的实现 |
| Ctrl-World | Ctrl-World 探索 controllability，DreamZero 探索 action generation |
| VLAW | VLAW 是 VLA+WM 协同，DreamZero 是 WM 吞掉 VLA |
| SimVLA | SimVLA 是端到端 VLA，DreamZero 是 world model as policy |

### 演化路径

```
WorldEval（能不能评）→ Ctrl-World（怎么控）→ DreamZero（直接做）
```

---

## 面试版一句话

> DreamZero 的核心洞察是：world model 如果能预测"未来的视频帧"，就能同时预测"应该采取的动作"，通过在想象中 rollout 多个候选动作并选择预期奖励最高的，实现无需训练的 zero-shot policy 迁移。

---

## 链接

- 论文: https://arxiv.org/abs/2401.04483
- 代码: https://github.com/dingdq/dreamzero
- VLA-Handbook: `theory/dreamzero_world_action_models_zero_shot_policies_2026.md`

---

_整理自 VLA-Handbook theory/dreamzero_world_action_models_zero_shot_policies_2026.md_
