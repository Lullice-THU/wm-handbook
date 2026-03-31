# WorldEval: World Model as Policy Evaluator — 深度解析

> **论文**: [arXiv:2412.04536](https://arxiv.org/abs/2412.04536)
> **核心问题**: World Model 能否作为 Policy Ranking Proxy？
> **关键词**: World Model, Policy Evaluation, Ranking, Simulation

---

## 一句话总结

WorldEval 证明了 **world model 可以作为 policy 版本排序的工具**，在真实机器人评测成本高昂的情况下，用 world model rollouts 筛选 policy 版本，大幅降低评测成本。

---

## 核心贡献

### 1. 解决的问题

**痛点**：评估 VLA/机器人 policy 需要：
- 真实机器人硬件
- 人工监督
- 大量 episode（每个任务 50-100 次）
- 每次评估成本：$500-$2000

**WorldEval 的方案**：
```
Policy A → World Model Rollouts → Ranking Score
Policy B → World Model Rollouts → Ranking Score
Policy C → World Model Rollouts → Ranking Score
        ↓
    选择最佳版本
```

### 2. 关键技术

**World Model Rollouts**：
- 给定初始 observation
- 让 world model "想象" 未来 50-100 步
- 评估想象轨迹的奖励/成功率

**Ranking Consistency**：
- WorldEval 排序与真实评测排序的一致性
- 关键指标：Kendall's τ > 0.7

### 3. 系统设计

```
┌─────────────────────────────────────┐
│           WorldEval System           │
├─────────────────────────────────────┤
│  1. World Model (Video + Physics)    │
│  2. Reward Predictor                 │
│  3. Ranking Aggregator               │
└─────────────────────────────────────┘
```

---

## 技术细节

### World Model 训练

| 参数 | 值 |
|------|-----|
| 数据 | 1M+ 机器人 episode |
| 预测窗口 | 50-100 步 |
| 评估任务 | 8 个 manipulation 任务 |

### Rollout 配置

| 参数 | 值 | 说明 |
|------|-----|------|
| rollout 长度 | 50 步 | 约 1 秒 |
| MC samples | 32 | 每个 policy |
| 评估任务数 | 8 | 抓取/放置/推动等 |

### 评估指标

| 指标 | 定义 | 目标 |
|------|------|------|
| Kendall's τ | 排序一致性 | > 0.7 |
| Spearman's ρ | 等级相关 | > 0.8 |
| NDCG@K | 前 K 排序质量 | > 0.85 |

---

## 实验结果

### 排序一致性

| 任务 | Kendall's τ | 真实评测成功率差 |
|------|-------------|-----------------|
| 抓取 | 0.82 | ±5% |
| 放置 | 0.78 | ±8% |
| 推动 | 0.71 | ±10% |
| 开关抽屉 | 0.85 | ±4% |
| 平均 | **0.79** | — |

**结论**：WorldEval 可以可靠地排序 policy 版本。

### 评测成本对比

| 方法 | 成本/版本 | 时间/版本 |
|------|----------|-----------|
| 真实机器人 | $1500 | 4 小时 |
| WorldEval | $0.5 | 2 分钟 |
| 加速比 | **3000×** | **120×** |

---

## 工程实现

### API 设计

```python
class WorldEvaluator:
    def rank_policies(self, policies, world_model, n_rollouts=32):
        """
        对多个 policy 版本排序
        
        Args:
            policies: List of policy checkpoints
            world_model: World model for rollouts
            n_rollouts: Number of MC samples per policy
        
        Returns:
            ranked_policies: List of (policy, score) sorted by score
        """
        scores = []
        for policy in policies:
            rollout_rewards = []
            for _ in range(n_rollouts):
                reward = self.single_rollout(policy, world_model)
                rollout_rewards.append(reward)
            scores.append(mean(rollout_rewards))
        
        return sorted(zip(policies, scores), key=lambda x: x[1], reverse=True)
```

---

## 局限性

1. **Good-looking ≠ Good evaluator**：视频质量高的 world model 不一定是好的 evaluator
2. **任务泛化**：只在 8 个 manipulation 任务上验证，泛化性未知
3. **物理准确性**：world model 对物体交互的物理建模不完美
4. **长 horizon**：对需要 >100 步的任务评估不可靠

---

## 与其他工作的关系

### 演化路径

```
WorldEval（能不能评）→ WorldArena（怎么统一评）→ Ctrl-World（怎么控）→ DreamZero（直接做）
```

### 相关工作

| 论文 | 关系 |
|------|------|
| WorldArena | WorldEval 的"评测框架版"，统一了 evaluator/planner/data engine |
| Ctrl-World | WorldEval 的"可控版"，加入 action conditioning |
| DreamZero | WorldEval 的"直接做版"，不需要 ranking，直接生成 action |

### Tension（核心张力）

> "Good-looking video ≠ Good evaluator"

这是 WorldEval → Ctrl-World/WorldArena 的核心推动力：
- 视频真 ≠ 策略排序准
- 能看出哪个 policy 强 ≠ 能稳定承担闭环 planning

---

## 面试版一句话

> WorldEval 解决了"评测太贵"的问题：用一个 world model 替代真实机器人做 policy 版本排序，3000× 成本降低，同时保持 0.79 的排序一致性（Kendall's τ）。

---

## 链接

- 论文: https://arxiv.org/abs/2412.04536
- VLA-Handbook: `theory/frontier/benchmarks/worldeval_world_model_policy_evaluator_2025.md`

---

_整理自 VLA-Handbook theory 目录_
