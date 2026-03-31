# DeepMind — 公司档案

> **官网**: deepmind.google
> **总部**: London, UK（Google DeepMind）
> **成立**: 2010（DeepMind），2023（与 Google Brain 合并）
> **母公司**: Alphabet

---

## 核心产品与技术

### Robotics 产品线

#### RoboCat — 自我改进的机器人代理
- **性质**: 自我改进的多臂机器人代理
- **创新**: 
  - 视觉-动作条件化的通才机器人
  - 能够在少量示例后泛化到新任务
  - 持续自我改进（类似 AlphaZero 思路）
- **数据**: 大量机器人数据自我生成

#### SIMA — 首个 Zero-Shot 游戏 Agent
- **性质**: Scalable Instructable Multiworld Agent
- **定位**: 3D 游戏环境中的通用 AI Agent
- **特点**:
  - 遵循自然语言指令
  - 跨多个 3D 游戏泛化
  - 类似具身 AI agent 在仿真世界中
- **与 WM 关系**: SIMA 探索在 3D 世界中的 instruction following = WM 应用场景

### 核心研究（机器人 + WM）

| 研究 | 方向 | 与 WM 关系 |
|------|------|-----------|
| **RT-2** | 视觉-语言-动作模型 | VLA = 隐式 WM |
| **RT-3** | RT-2 升级版 | 更强泛化 |
| **RT-X** | 跨机器人通才 | 多本体 WM |
| **DeepMind Robotics** | 仿真到真实迁移 | SIMP, RL 算法 |
| **Sputnik/MuZero** | 世界模型（游戏）| AlphaZero 系列 = WM 先驱 |
| **Genie** | 视频生成 + 动作控制 | 视频作为 WM |

### DeepMind 的 World Model 路线

**三层世界模型架构**:

| 层 | DeepMind 工作 | 说明 |
|---|-------------|------|
| **游戏 WM** | MuZero, AlphaZero | 棋类/游戏世界建模 |
| **视频 WM** | Genie, W.A.F.F.L.E. | 视频作为潜在动作模型 |
| **具身 WM** | RT-2/3, RoboCat, SIMA | VLA 作为隐式 WM |

**关键创新**:
1. **Genie**: 从视频中推断潜在动作空间（类 WM）
2. **RT-2**: 将 LLM/VLM 能力泛化到机器人动作
3. **SIMA**: 3D 世界中的 instruction following agent

---

## 技术路线分析

| 组件 | 角色 | 技术 |
|------|------|------|
| **RT-2/3** | VLA 基座 | 视觉+语言→动作 |
| **MuZero** | 游戏 WM | 隐式世界建模 |
| **Genie** | 视频 WM | 潜在动作推断 |
| **SIMA** | 3D Agent | 仿真世界 agent |
| **RoboCat** | 通才机器人 | 自我改进 RL |

---

## Google 整体机器人布局

DeepMind 是 Google/Alphabet 机器人布局的核心：

| 实体 | 方向 |
|------|------|
| **DeepMind** | 基础研究 + 算法 |
| **Google Robotics** | 实物机器人 |
| **Everyday Robots** | 已合并入 DeepMind |
| **Intrinsic** | 工业机器人软件（Alphabet 子业务）|

---

## 关键人物

| 姓名 | 角色 | 背景 |
|------|------|------|
| Demis Hassabis | CEO / Co-founder | DeepMind 创始人，认知神经科学背景 |
| Koray Kavukcuoglu | CTO | 深度学习研究负责人 |
| 机器人团队 | 负责人 | 多位 RL/机器人研究者 |

---

## DeepMind 的 WM 特点分析

**与其他公司的关键区别**:

| 公司 | WM 路线 | 特点 |
|------|---------|------|
| **DeepMind** | 游戏+视频+具身三层WM | 最系统化的 WM 研究 |
| **1X** | 明确 WM 为认知核心 | 工程化路线 |
| **PI** | Genesis + Action Model | 仿真数据路线 |
| **Figure** | 端到端 VLA | 依赖 OpenAI |

**DeepMind 的独特优势**:
1. **MuZero/AlphaZero**: 世界模型理论基础最扎实
2. **Genie**: 视频 → 潜在动作 = WM 新范式
3. **Google 资源**: TPU + 大规模 RL + 仿真器

**核心洞见**: DeepMind 是唯一一个在"游戏 WM"(MuZero) → "视频 WM"(Genie) → "具身 WM"(RT-2/SIMA) 有完整路线图的公司。

---

## 快速结论

```
一句话: DeepMind 拥有最系统化的 World Model 研究路线，
        从 MuZero（游戏）→ Genie（视频）→ RT-2/SIMA（具身），
        是 World Model 学术研究和工业应用的桥头堡。

核心路线: 游戏WM → 视频WM → 具身VLA，三层递进
关键优势: AlphaZero/MuZero 理论积累 + Google TPU + 仿真器
WM 地位: 学术界 + 工业界 WM 领袖
产品状态: 研究导向，RT-2/3/Genie/SIMA 尚未商业化
```

---

_整理: WM Research OPC | 2026-04-01_

## 参考链接

- [DeepMind Robotics](https://deepmind.google/robots)
- [RT-2](https://robotics-transformer.github.io)
- [SIMA](https://deepmind.google/sima)
- [Genie](https://deepmind.google/genie)
