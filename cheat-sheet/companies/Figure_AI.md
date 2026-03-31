# Figure AI — 公司档案

> **官网**: figure.ai
> **总部**: Sunnyvale, CA
> **成立**: 2022
> **融资**: ~$675M (B轮$125M + 微软等$700M)
> **估值**: $26B (2025)

---

## 核心产品与技术

### Figure 01 — 通用人形机器人
- **发布**: 2023
- **硬件**: 人形，双臂，轮式底盘
- **AI**: 端到端 VLA，OpenAI 合作

### Figure 02 — 升级版人形
- **发布**: 2024
- **升级**: 更强 AI 能力，更长续航

### Helix — Figure 的 VLA/WorldModel 方向
- **性质**: 具身大模型项目
- **特点**: "人形机器人通用具身模型"
- **与 WM 关系**: 
  - Figure 明确研究 WM 用于机器人控制
  - Helix 可能包含 world modeling 能力（未完全公开）
- **OpenAI 合作**: 提供多模态 LLM 支持

###  BMW 合作 — 工业落地
- 2023年宣布与 BMW 合作，在汽车生产线部署 Figure 机器人
- 目标：替代部分流水线人工操作

---

## 技术路线

| 方向 | 具体工作 | 与 WM 关系 |
|------|---------|-----------|
| VLA | 端到端视觉-动作 | 核心产品 |
| LLM 集成 | OpenAI 多模态模型 | 感知/推理基座 |
| 仿真 | 部分内部仿真能力 | 潜在 WM 方向 |
| 硬件 | 人形机器人制造 | 落地载体 |

---

## 关键人物

| 姓名 | 角色 | 背景 |
|------|------|------|
| Brett Adcock | Founder / CEO | Archer Aviation, V41 Ventures |
| Jerry Pratt | CTO | IHMC（MIT spin-off）|
| Jon Dykton | Head of AI | OpenAI, Tesla |

---

## Figure 的 WM 路线分析

Figure 选择了与 PI 不同的路线：
- **PI**: 分立（WM + Action Model 分开）
- **Figure**: 端到端 VLA（OpenAI LLM + 动作输出联合建模）

**潜在问题**：
- 端到端 VLA 缺乏显式 world model → 可解释性差
- 但 Figure + OpenAI 合作可能在 LLM 层面隐式建模

**Figure 的 WM 潜力**：
- OpenAI 模型有强大的 world modeling 能力（视频生成 Sora 等）
- Figure 可能在探索将 Sora 类能力迁移到机器人

---

## 快速结论

```
一句话: Figure AI 是估值最高的人形机器人公司（$26B），走端到端 VLA 路线，
        与 OpenAI 深度合作，正在探索 LLM 隐式 world modeling 在机器人控制中的应用。

估值: $26B（全球最高估值人形机器人公司）
核心路线: 端到端 VLA（OpenAI LLM 加持）
BMW 落地: 工业场景真实部署
WM 方向: 依赖 OpenAI 隐式 world modeling，未公开 WM 专项研究
```

---

_整理: WM Research OPC | 2026-03-31_
