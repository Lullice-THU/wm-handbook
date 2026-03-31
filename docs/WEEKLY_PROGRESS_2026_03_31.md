# World Model 研究周报

**报告期:** 2026-03-24 ~ 2026-03-31
**生成时间:** 2026-03-31
**OPC:** wm-research
**知识库:** VLA-Handbook (github.com/sou350121/VLA-Handbook)

---

## 📊 本周仓库活跃度概览

| 指标 | 数据 |
|------|------|
| 本周新增理论论文 | **9 篇** |
| 本周新增深度解析 | **5 篇** |
| GitHub Stars | 106（稳定） |
| 知识库文档 | 9 文件完整 |

### 本周 Commit 时间线

```
03-31 16:35  SOMA — Strategic Orchestration + Memory Augmentation
03-31 15:35  COMO — Continuous Latent Motion from Internet Videos
03-31 14:05  Wanderland — Geometrically Grounded Open World Simulation
03-31 13:19  BeSafe-Bench — 四域行为安全基准 ⭐
03-31 12:33  VLA-OPD — SFT/RL Bridge with Reverse KL ⭐
03-30 15:36  ViFailback — Visual Symbols for Failure Diagnosis ⭐
03-28 16:34  UCPE — Unified Camera Positional Encoding
03-27 21:42  Beyond Attention Magnitude (inter-layer rank)
03-27 21:03  VideoWeaver — Multi-View Video-to-Video Transfer
03-27 19:41  UCPE — Unified Camera Positional Encoding
03-27 19:21  ARTPRO — Articulated Object Reconstruction
```

---

## 📄 本周新增论文详解

### ⭐ Tier 1 — 高价值论文（必读）

#### 1. BeSafe-Bench（2026-03-31）
**BeSafe-Bench: Unveiling Behavioral Safety Risks of Situated Agents**

| 维度 | 数据 |
|------|------|
| 论文 | arXiv:2603.25747 |
| 定位 | 首个四域统一行为安全基准（Web/Mobile/Embodied VLM/VLA） |
| 任务规模 | 1312 任务 |
| 安全风险类别 | 9 类 |
| 评估指标 | SR + SafetyR + S-S 联合分佈 |

**核心发现：**
- 13个主流代理中，**最佳者 S-S（成功且安全）率 < 40%**
- **41% 的"成功"任务同时触发了安全风险**（S-U: Success but Unsafe）
- GPT-5 (Embodied VLM): SR=65.84%, SafetyR=30.43%, S-U=**40.99%**
- 关键洞察：任务能力与安全鲁棒性之间存在**系统性脱节**

**为什么重要：** 安全不能依赖"更强的模型"，需要专门的对齐机制。这是首个覆盖完整四域的 VLA 安全评估基准。

---

#### 2. VLA-OPD（2026-03-31）
**VLA-OPD: Bridging Offline SFT and Online RL via On-Policy Distillation**

| 维度 | 数据 |
|------|------|
| 论文 | arXiv:2603.26666 |
| 核心创新 | 反向 KL 散度的 on-policy 蒸馏 |
| 关键数字 | 1-traj 初始化达 **87.4%** 成功率（逼近全量 SFT 的 87.9%）|
| 叠加 GRPO | 恢复教师 99% 性能（93.4% vs 93.9%）|

**核心洞察：**
- 反向 KL 的"模式寻求"特性 → 避免 Forward-KL 熵爆炸 + Hard-CE 熵坍缩
- 适用：有教师模型 + 需要快速适配新任务 + 担心 SFT 灾难性遗忘
- 不能做：无教师模型时无法使用；仍需环境交互（非纯离线）

**为什么重要：** 首次系统性地用反向 KL 解决 SFT→RL 迁移中的效率-鲁棒性矛盾，为 VLA 后训练提供了新范式。

---

#### 3. Wanderland（2026-03-31）
**Wanderland: Geometrically Grounded Simulation for Open World**

| 维度 | 数据 |
|------|------|
| 核心创新 | 几何 grounding 的开放世界仿真平台 |
| 解决的问题 | 开放世界机器人训练中高保真度几何建模 |

**为什么重要：** 开放世界机器人训练的核心瓶颈是几何一致性问题（穿模、物体关系错误），Wanderland 提供了系统性的几何 grounding 解决方案。

---

### Tier 2 — 中等价值论文（值得了解）

#### 4. ViFailback（2026-03-30）
**Diagnose, Correct, and Learn from Manipulation Failures via Visual Symbols**

- **核心创新**：7种视觉符号（箭头、十字准星、ON/OFF标签等）标注失败视频
- **数据**：5,202条真实ALOHA双臂机器人轨迹，58,128 VQA对
- **效果**：真实世界 VLA 任务成功率提升 **22.2%**
- **洞察**：视觉符号是人机高效通信协议，比纯文本标注快 2.5×

#### 5. COMO（2026-03-31）
**COMO: Learning Continuous Latent Motion from Internet Videos**

- **核心创新**：从互联网视频学习连续潜在动作
- **解决的问题**：互联网视频中的动作表示学习（无需人工标注）

#### 6. SOMA（2026-03-31）
**SOMA: Strategic Orchestration and Memory-Augmented System**

- **核心创新**：战略编排 + 记忆增强的系统设计
- **解决的问题**：多任务场景下的长期记忆和战略规划

---

### Tier 3 — 技术模块论文（按需阅读）

| 论文 | 日期 | 方向 |
|------|------|------|
| UCPE | 03-28 | 统一相机位置编码（射线级），视频生成控制 |
| Beyond Attention Magnitude | 03-27 | 层间秩一致性，Transformer 压缩 |
| VideoWeaver | 03-27 | 多视角视频迁移，跨视角一致性 |
| ARTPRO | 03-27 | 关节物体自监督重建，无标注学习 |

---

## 🎯 3个最有价值的研究方向

### 🥇 第一名：VLA 安全对齐（Safety Alignment）

**推荐理由：**
- BeSafe-Bench 数据揭示了当前 VLA 的**系统性安全缺陷**：41% 的成功任务伴随安全风险
- 这是 2026 年最具实用价值的研究方向——不解决安全问题，VLA 无法部署到真实场景
- S-U（成功但不安全）问题在 GPT-5 等顶级模型上高达 40.99%

**关键论文：**
1. BeSafe-Bench（基准 + 问题定义）
2. IS-Bench（具身交互安全，161场景）
3. VLA Intrinsic Safety（内在安全机制）

**切入角度：**
- 如何在 VLA 训练中引入安全约束（而非事后添加）
- 过程安全 vs 终止安全（中间步骤 vs 最终状态）
- 复合风险场景下的安全退化问题

---

### 🥈 第二名：VLA 后训练效率（SFT → RL 桥接）

**推荐理由：**
- VLA-OPD 证明了反向 KL + On-Policy 蒸馏可以在极少数据（1-traj）下达到接近全量 SFT 的效果
- 这解决了 VLA 落地最大的工程瓶颈：**真实机器人数据稀缺**
- 方向明确：有教师模型时用反向 KL；无教师时需要探索其他范式

**关键论文：**
1. VLA-OPD（核心方法）
2. AtomVLA（Predictive WM + Offline RL）
3. SimpleVLA（极简基线对比）

**切入角度：**
- 反向 KL vs Forward KL vs Hard-CE 的理论分析
- On-policy 蒸馏的具体工程实现
- 多任务场景下的灾难性遗忘问题

---

### 🥉 第三名：世界模型的长程一致性（Long-Horizon WM Consistency）

**推荐理由：**
- MIND 论文揭示：当前 WM 在 >50 帧后一致性显著下降（ℒ_lcm 从 0.10→0.31）
- 记忆一致性是开放世界机器人的核心挑战
- COMO 和 SOMA 本周新增论文都指向这个方向（连续动作建模 + 记忆增强）

**关键论文：**
1. MIND（记忆一致性基准，Research Gap #1）
2. COMO（连续潜在动作学习）
3. SOMA（战略编排 + 记忆增强）
4. ENACT（具身认知 + 自我中心 WM）

**切入角度：**
- 环路一致性测试（向前→原路返回→MSE 比较）
- 多模态记忆表示（视觉 + 动作 + 物理属性）
- 开放世界下的几何 grounding（Wanderland）

---

## 📈 研究趋势总结

| 趋势 | 描述 | 置信度 |
|------|------|--------|
| **安全先行** | 安全对齐从"nice to have"变成"must have"，S-U 问题受到前所未有重视 | ⭐⭐⭐ |
| **后训练效率** | 少样本、离线数据驱动的 VLA 后训练成为工程落地关键 | ⭐⭐⭐ |
| **多域统一评估** | 从单域评测走向 Web+Mobile+Embodied VLM+VLA 四域统一基准 | ⭐⭐⭐ |
| **连续动作建模** | 从离散动作走向连续潜在动作（COMO、OLAF） | ⭐⭐ |
| **几何 grounding** | 开放世界仿真的核心瓶颈（穿模、物体关系） | ⭐⭐ |

---

## ⚠️ 待深入研究

1. **CLAUDE.md**（新增）：仓库新增的"对抗性思辩"研究范式，值得了解
2. **adversarial-research-analyst/** 和 **book/** 目录（新增）：仓库新增的基础设施
3. **VLA-Arena**：对比 BeSafe-Bench 的 VLA 专用评测平台

---

## 📚 参考文献

- BeSafe-Bench: https://arxiv.org/abs/2603.25747
- VLA-OPD: https://arxiv.org/abs/2603.26666
- ViFailback: https://arxiv.org/abs/2512.02787
- MIND: https://arxiv.org/abs/2602.08025
- IS-Bench: https://arxiv.org/abs/2506.16402
- VLA-Handbook: https://github.com/sou350121/VLA-Handbook

---

*报告生成：OPC wm-research Agent | 数据来源：VLA-Handbook GitHub API*
