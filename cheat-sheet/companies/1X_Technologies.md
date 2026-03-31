# 1X Technologies — 公司档案

> **官网**: [1x.tech](https://www.1x.tech)
> **总部**: San Carlos, CA
> **成立**: 2014 (原 Halodi Robotics)
> **融资**: $125M+ (包括 EQT Ventures, SK联合等)

---

## 核心产品与技术

### NEO — 家用人形机器人
- **发布**: 2024 (Early Access)
- **定位**: 家用服务机器人，主打日常家务自动化
- **硬件参数**:
  - 身高: 5'6" (167cm)
  - 体重: 66 lbs (30kg)
  - Lift: 154 lbs | Carry: 55 lbs | Arm Payload: 18 lbs
  - 自由度数: 手臂7×2, 双手22×2, 颈部3, 脊柱2, 腿部6×2
  - 最高速度: 6.2 m/s (跑步), 1.4 m/s (行走)
  - 电池: 842 Wh, 4小时续航, 6min快充
- **安全设计**: 软体外壳(3D lattice聚合物), 肌腱驱动, 零夹点, HIC<250
- **价格**: $200 订金预订

### Redwood AI — 机器人基础模型
- **性质**: VLA (Vision-Language-Action Model)
- **功能**: 
  - 移动+操作联合控制(步行、坐立、跪、爬楼梯)
  - 视觉导航和物体操作
  - 集成语音预测用户意图
- **特点**: 成功和失败数据都用于学习

### World Model — 1X 的世界模型 ⭐
- **性质**: 视频生成模型，基于物理约束
- **定位**: NEO 的"认知核心"(cognitive core)
- **核心能力**:
  - **预测/幻觉**: 在真实行动前预测动作结果
  - **泛化**: 对未见过的任务实现零样本泛化
  - **学习**: Expert Mode 下远程专家指导学习新技能
- **与 Redwood 分工**: WM 做预测规划, Redwood 做执行控制

---

## 技术路线分析

| 组件 | 角色 | 技术 |
|------|------|------|
| **World Model** | 认知/预测/泛化 | 视频生成 + 物理先验 |
| **Redwood AI** | VLA 控制器 | 视觉-语言-动作联合 |
| **Expert Mode** | 远程辅导学习 | 人机协作 |
| **NEO 硬件** | 身体执行 | 肌腱驱动软体机器人 |

---

## 关键人物

| 姓名 | 角色 | 背景 |
|------|------|------|
| Bernt Børnich | CEO/Founder | 多年机器人创业 |
| Marc Raibert | Advisor | Boston Dynamics 创始人 |
| (招募中) | WM 研究团队 | 正在招聘 WM 研究工程师 |

---

## 1X 的 WM 路线特点

**与 PI/Figure 的关键区别**:

| 公司 | WM 定位 | 路线 |
|------|---------|------|
| **1X** | 明确 WM 为认知核心 | WM(video) + VLA(Redwood) 分层 |
| PI | Genesis 做数据引擎 | WM(仿真) + Action Model 分立 |
| Figure | 依赖 OpenAI 隐式建模 | 端到端 LLM |

**1X 的创新点**:
1. **显式 World Model**: 直接宣称 WM 是"认知核心"
2. **物理 grounding**: WM 是"grounded in physics"的视频模型
3. **预测驱动**: WM 用于预测行动结果，实现"先想后做"
4. **泛化引擎**: WM 驱动零样本任务泛化

---

## 对 WM 研究的启示

1X 提供了**最清晰的 WM 应用范式**:
```
World Model = 预测 + 泛化 + 物理先验
Redwood = 移动 + 操作 + 人机协作
NEO = 硬件载体
```

**核心洞见**: 1X 的 WM 不是生成视频娱乐，而是**具身决策的前置模块**——在动作执行前预测结果，实现安全可控的泛化。

---

## 快速结论

```
一句话: 1X 是唯一明确将 World Model 作为"认知核心"的机器人公司，
        其 WM(video+physics) 驱动 Redwood VLA 执行，代表当前最清晰的
        WM 具身应用架构。

融资: $125M+
核心创新: WM 做预测/泛化, Redwood 做执行, 分层协同
产品状态: NEO Early Access 阶段
技术亮点: 物理 grounded 视频 WM + 肌腱驱动软体机器人
```

---

_整理: WM Research OPC | 2026-03-31_

## 参考链接

- [1X AI 页面](https://www.1x.tech/ai)
- [NEO 产品页面](https://www.1x.tech/neo)
- [World Model 演示](https://youtu.be/lS_z60kjVEk)
- [Redwood AI 介绍](https://www.1x.tech/discover/redwood-ai)
