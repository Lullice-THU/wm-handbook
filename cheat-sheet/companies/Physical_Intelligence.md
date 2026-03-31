# Physical Intelligence (PI) — 公司档案

> **官网**: physicalintelligence.com
> **总部**: San Francisco, CA
> **成立**: 2023
> **融资**: ~$400M (A轮$70M + B轮$300M+)

---

## 核心产品与技术

### π0 (Pi-Zero) — 通用机器人基础模型
- **发布**: 2024
- **定位**: 通用动作模型（Action Model），非 World Model
- **架构**: Diffusion policy + VLA backbone
- **特点**: 跨形态泛化，支持手臂/双腿/轮式

### π0.5 — 能力升级版
- **更新**: 2024年底
- **改进**: 更强泛化 + 自我改进能力（Recap）

### Genesis — 机器人基础模型套件
- **发布**: 2024
- **包含**: Genesis-1/2/3 系列
- **核心**: 物理引擎 + 生成式数据 + 机器人策略
- **创新**: 用生成式物理仿真替代真实数据

### 3.1 **World Model 关联**: Genesis-π
- Genesis 作为数据引擎生成多样化仿真轨迹
- π0 作为 action model 消费这些数据
- 形成 **WM(Genesis) + Action Model(π0)** 分工

---

## 研究方向

| 方向 | 代表工作 | 与 WM 关系 |
|------|---------|-----------|
| Action Model | π0, π0.5 | 直接输出动作，非 WM |
| 仿真数据 | Genesis | WM 生成仿真轨迹 |
| 物理引擎 | Genesis Physics | WM 环境建模 |
| 模仿学习 | Behavior Cloning | 数据来源 |
| 强化学习 | on-policy adaptation | π0 自我改进 |

---

## 关键人物

| 姓名 | 角色 | 背景 |
|------|------|------|
| Karol Hausman | Co-founder / CEO | Google Brain, Stanford |
| Chelsea Finn | Co-founder | Stanford, IRIS |
| Pieter Abbeel | Co-founder / Advisor | UC Berkeley, Covariant |
| Sergey Levine | Advisor | UC Berkeley |
| Vikash Kumar | Research Lead | CMU, Columbia |

---

## 对 WM 方向的启示

PI 选择了 **"分立架构"** 而非 "大一统 WM"：
- Genesis（WM生成）↔ π0（Action执行）分立
- 优势：各模块可独立迭代
- 劣势：WM→Action 的信息传递有损失

**这是当前主流路线**：WM 做评测/仿真，Action Model 做执行。

---

## 快速结论

```
一句话: PI 是"分立路线"代表——Genesis做WorldModel，π0做ActionModel，
        两者分工而非融合，代表当前工业界主流选择。

融资规模: ~$400M（最大 VC 支持的机器人 AI 公司之一）
核心技术: Diffusion Policy + 生成式仿真
WM 定位: Genesis 扮演数据引擎角色，非端到端 WM
```

---

_整理: WM Research OPC | 2026-03-31_
