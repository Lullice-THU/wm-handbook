# WorldModel 技术主线：从 Evaluator 到 Planner，再到 World Action Model

> 整理自: [VLA-Handbook - world_model_mainline.md](https://github.com/sou350121/VLA-Handbook/blob/main/theory/world_model_mainline.md)
> 
> 核心问题: WorldModel 在 VLA / Embodied AI 里，正在从"视频模型"演化成什么？

---

## 1. 核心问题

WorldModel 在机器人里，过去常说一句话：
> "让模型学会预测未来"

但落到系统里，关键问题是：
- 它是拿来**评策略**的？（Evaluator）
- 还是拿来**替代环境 rollout**的？（Environment Proxy）
- 还是拿来**生成数据/动作**的？（Data Engine / Action Model）
- 它最后是辅助 policy，还是干脆开始**吞掉 policy 的角色**？

---

## 2. 技术主线：四阶段演化图

```
┌──────────────────────────────────────────────┐
│ 1) Evaluator 起点：WorldEval                │
│ "能不能先用 world model 排策略、筛版本？"   │
└──────────────────────┬───────────────────────┘
                      │ 先解决 ranking proxy 问题
                      ▼
┌──────────────────────────────────────────────┐
│ 2) 统一评测口径：WorldArena                  │
│ "world model 不只比像不像，还要比功能。"    │
└──────────────────────┬───────────────────────┘
                      │ 把 evaluator / planner / data engine
                      │ 写成统一 benchmark
                      ▼
┌──────────────────────────────────────────────┐
│ 3) 更强模型路线：Ctrl-World                  │
│ "如果 world model 足够 controllable，       │
│  它就更像一个可用 imagination env。"         │
└──────────────────────┬───────────────────────┘
                      │ 从评测器走向 policy-in-the-loop
                      ▼
┌──────────────────────────────────────────────┐
│ 4) 更激进终点：DreamZero / WAM               │
│ "world model 不只辅助 policy，               │
│  而是开始和 action model 融成一体。"       │
└──────────────────────────────────────────────┘
```

**一句话总结:**

WorldEval 在问"能不能先评"，WorldArena 在问"到底该怎么统一评"，Ctrl-World 在答"什么样的 world model 更像可用环境"，DreamZero 则进一步问"既然都能预测世界了，为什么不顺手把动作也一起学掉？"

---

## 3. 四个关键节点

| 层级 | 文章 | 回答什么问题 | 关键贡献 |
|------|------|-------------|---------|
| 1 | WorldEval | world model 能否做 policy ranking proxy？ | 把 world model evaluator 做成可操作系统 |
| 2 | WorldArena | world model 应该如何统一评测？ | 把 Data Engine / Policy Evaluator / Action Planner 写进 benchmark |
| 3 | Ctrl-World | 什么样的 world model 更适合 policy-in-the-loop？ | multi-view + frame-level action conditioning + memory retrieval |
| 4 | DreamZero | world model 是否会吞掉 action model？ | 把 WAM 写成联合预测 video + action 的主监督框架 |

---

## 4. WorldModel 角色升级三阶段

### 阶段 A: world model = 离线评测器
```
policy checkpoints ──> world model rollouts ──> ranking / filtering
```

### 阶段 B: world model = 环境代理
```
policy ──> imagined rollout ──> candidate actions / synthetic data
                              │
              └──────────────────────> real env verification
```

### 阶段 C: world model = 动作生成基底
```
observation + goal
        │
        ▼
  world action model
   ├─ predict future video
   └─ predict action chunk
        │
        ▼
  closed-loop control
```

---

## 5. 三个核心张力

### 5.1 Good-looking video ≠ Good evaluator
> WorldEval → WorldArena 的核心张力
- 视频真 ≠ 策略排序准

### 5.2 Good evaluator ≠ Good planner
> WorldEval → Ctrl-World / WorldArena 的核心张力
- 能看出哪个 policy 强 ≠ 能稳定承担闭环 planning

### 5.3 World model ≠ Auxiliary module
> Ctrl-World → DreamZero 的核心张力
- 一开始它只是 evaluator / proxy
- 后来它越来越像 policy substrate 本身

```
角色演化路径:
side module → system tool → core control substrate
```

---

## 6. 核心论文详解

### 6.1 WorldEval（Evaluator 起点）

**论文**: WorldEval: World Model as Policy Evaluator

**核心贡献**: 把 world model evaluator 做成可操作系统

**关键问题**: world model 能否做 policy ranking proxy？

**链接**: `theory/frontier/benchmarks/worldeval_world_model_policy_evaluator_2025.md`

---

### 6.2 Ctrl-World × WorldArena（走向可控环境）

**论文**: Ctrl-World + WorldArena

**核心贡献**: 
- multi-view + frame-level action conditioning + memory retrieval
- 把 Data Engine / Policy Evaluator / Action Planner 写进统一 benchmark

**关键问题**: 什么样的 world model 更适合 policy-in-the-loop？

**链接**: `theory/frontier/benchmarks/ctrl_world_worldarena_embodied_world_model_benchmark_2026.md`

---

### 6.3 DreamZero（动作模型合一）

**论文**: DreamZero: World Action Models Are Zero-Shot Policies

**核心贡献**: 把 WAM 写成联合预测 video + action 的主监督框架

**关键洞察**: 
- world model 已经可以预测"未来的视频帧"
- 如果同时预测 action chunk，就变成了 World Action Model
- Zero-shot transfer 能力来自 joint modeling

**链接**: `theory/dreamzero_world_action_models_zero_shot_policies_2026.md`

---

### 6.4 WAM（Video Pretraining 三路线）

**论文**: WAM: Three Routes to Video Pretraining

**核心贡献**: 梳理视频预训练的三条路线对比

**链接**: `theory/frontier/wam_three_routes_video_pretraining_vs_vla_2026.md`

---

### 6.5 VLAW（VLA + WM 协同）

**论文**: VLAW: Iterative Co-Improvement VLA + World Model

**核心贡献**: VLA 和 WorldModel 协同迭代改进

**链接**: `theory/frontier/vlaw_iterative_co_improvement_vla_world_model_2026.md`

---

### 6.6 AtomVLA（Predictive World Models）

**论文**: AtomVLA: Offline Post-Training + Predictive World Models

**核心贡献**: 离线后训练结合预测性世界模型

**链接**: `theory/frontier/atomvla_offline_post_training_predictive_latent_world_models_2026.md`

---

### 6.7 GigaBrain（World Model RL）

**论文**: GigaBrain: World Model RL Ramp (0.5M Stars)

**核心贡献**: 世界模型强化学习规模化训练

**链接**: `theory/gigabrain_0_5m_star_world_model_based_rl_ramp_2026.md`

---

### 6.8 Causal World Modeling

**论文**: Causal World Modeling for Robot Control

**核心贡献**: 因果世界建模用于机器人控制

**链接**: `theory/causal_world_modeling_for_robot_control_dissection.md`

---

## 7. 系统插槽图

### 传统 VLA 闭环
```
obs ──> VLA policy ──> action ──> real world ──> next obs
```

### 加上 Evaluator 之后
```
obs ──> VLA policy ──> action ──> real world ──> next obs
                │
                └────────────> world model evaluator
                   └─ rank / diagnose / screen
```

### 加上 Proxy Environment 之后
```
obs ──> policy ──> imagined rollout in world model ──> action plan
              │                                        │
              └──────────────────── real world <────────┘
```

### 走到 WAM 之后
```
obs + goal ──> WAM
 ├─ future video
 └─ action chunk
        │
        ▼
  real world
```

---

## 8. 与其他主线的关系

### 与 VLA 研究主线的关系

| VLA 研究主线 | WorldModel 主线 |
|-------------|----------------|
| 怎么把 policy 做强 | 怎么让系统拥有想象、评测与预测环境能力 |
| 数据 / 感知 / 后训练 | Evaluator / Planner / WAM |
| 偏 agent 训练 | 偏 agent 外层能力与系统工具 |

- VLA 主线 = **训练主线**
- WorldModel 主线 = **世界代理主线**

### 与 Benchmark 主线的关系

| Benchmark 主线 | WorldModel 主线 |
|--------------|----------------|
| world model 是"评测体系的一层" | world model 是"系统功能角色本身" |
| 关心怎么定义 benchmark / evaluator | 关心怎么变成 evaluator / planner / WAM |
| 偏结构与问题定义 | 偏角色演化与技术路线 |

---

## 9. 推荐阅读路线

### A) 理解"WorldModel 为什么先从 Evaluator 起步"
1. WorldEval
2. Ctrl-World × WorldArena

→ 建立现实感：真机评测太贵 → evaluator 是第一个最刚需的落点

### B) 理解"WorldModel 如何从评测器变成环境代理"
1. WorldEval
2. Ctrl-World × WorldArena
3. DreamZero

→ 看到演化：evaluator → proxy environment → WAM/action-generating model

### C) 理解"DreamZero 到底新在哪"
1. Ctrl-World × WorldArena
2. DreamZero

→ 先理解 controllability 和 functional utility，再看 video + action joint modeling

---

## 10. 面试版一句话总结

> world model 在机器人里最早常被当成未来预测器，
> 但真正有工程价值的第一步其实是 evaluator，
> 所以 WorldEval 先解决"能不能保持策略排序一致"；
> 随后 WorldArena 把 world model 的功能角色正式写成 benchmark，
> Ctrl-World 则代表更强的 action-conditioned、policy-in-the-loop 路线，
> 而 DreamZero 更进一步，把 world model 和 action model 合成 WAM，
> 说明 world model 正在从评测工具演化成控制系统的一部分。

---

## 11. 研究空白（待补充）

- 更多 evaluator work：追踪 world model ranking proxy 是否真的稳
- 更多 planner / data engine work：WorldModel 作为合成数据引擎的案例
- 更强 WAM / unified model work：video+action 联合建模路线
- 与 evaluation.md 更明确对接：回答"什么时候必须回真机"

---

## 📎 关键链接汇总

| 资源 | 链接 |
|------|------|
| WorldModel 主线总纲 | `theory/world_model_mainline.md` |
| VLA 研究主线 | `theory/vla_research_mainline.md` |
| Benchmark 主线 | `theory/frontier/benchmarks/benchmark_mainline.md` |
| 评估体系 | `theory/evaluation.md` |
| 论文索引 | `theory/paper_index.md` |
| DreamZero | `theory/dreamzero_world_action_models_zero_shot_policies_2026.md` |
| WorldEval | `theory/frontier/benchmarks/worldeval_world_model_policy_evaluator_2025.md` |
| Ctrl-World | `theory/frontier/benchmarks/ctrl_world_worldarena_embodied_world_model_benchmark_2026.md` |
