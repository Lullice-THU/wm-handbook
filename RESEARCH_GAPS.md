# 研究空白与机会分析

> 基于 VLA-Handbook 深度分析 + 社区实战笔记
> 整理日期: 2026-03-30

---

## 1. WorldModel 方向的研究空白

### 1.1 Evaluator 的稳定性问题

**现状**: WorldEval 证明 world model 可以做 policy ranking proxy

**空白**:
- ranking proxy 是否真的稳定？（缺乏大规模验证）
- 不同任务类型下 evaluator 准确性差异有多大？
- 如何构建一个通用 evaluator 而非 per-task evaluator？

**链接参考**: `theory/world_model_mainline.md` — "good-looking video ≠ good evaluator"

---

### 1.4 World Model 的记忆一致性问题（基于 MIND 深度解析）

**现状**: MIND benchmark（2026-02）首次系统评估 WM 长程记忆，发现当前模型在>50帧后一致性显著下降

**关键数据**:
- ℒ_lcm（长程记忆）：当前最优模型在>50帧预测时 MSE 从 0.10→0.31（显著衰减）
- ℒ_gsc（环路一致性）：向前→返回环路存在累积误差，几何不稳定
- RPE（动作精度）：跨动作空间泛化时，有记忆反而比无记忆更差（干扰推理）
- 第三人称角色穿模：缺乏显式碰撞检测，角色-背景交互失效

**核心问题**:
1. **长程记忆漂移**：上下文窗口有限，早期信息丢失，>100帧预测几乎不可信
2. **动作-记忆干扰**：当测试动作空间与训练不一致时，记忆上下文反而干扰推理
3. **环路不一致**：世界模型非确定性生成导致累积误差，闭环测试失败
4. **碰撞检测缺失**：仅靠视觉生成无法保证几何一致性

**研究机会**:
- 设计记忆压缩/选择性遗忘机制，保持关键信息同时减少干扰
- 动作空间自适应检测 + 记忆条件解除
- 引入显式几何约束（深度图/占用网格）而非纯视觉生成
- 建立记忆-动作解耦的训练目标

**链接**: MIND paper — arXiv:2602.08025 | 代码: github.com/CSU-JPG/MIND

---

### 1.2 World Model 的数据引擎角色

**现状**: World model 作为合成数据生成器的案例还不够丰富

**空白**:
- 合成数据的多样性如何保证？
- World model 生成数据 vs 真实机器人数据的 gap 有多大？
- 如何验证生成数据的质量？

**链接参考**: `theory/vla_research_mainline.md` — "数据规模化" 方向

---

### 1.3 WAM 的边界问题

**现状**: DreamZero 把 world model 和 action model 合一

**空白**:
- 什么场景下 WAM 比专用 policy 更好？
- WAM 的 zero-shot 泛化边界在哪？
- joint video + action modeling 的训练稳定性问题

**链接参考**: 
- `theory/dreamzero_world_action_models_zero_shot_policies_2026.md`
- `theory/world_action_models_are_zero_shot_policies_dissection.md`

---

## 2. VLA 训练方向的研究空白

### 2.1 动作空间对齐

**现状**: Sim2Real 是 VLA 最大的工程难题

**空白**:
- 动作空间的语义对齐（不同机器人形态之间的动作语义差异）
- 触觉/力控信号的融合方式没有统一标准
- 高频控制（50Hz+）下的动作预测精度问题

**社区洞察**（来自小红书中文社区）:
> "ACT 50 episodes 就能 work、Sim2Real 八成是物理参数没校准"

**链接**: `theory/frontier/taf_vla_tactile_force_alignment_2026.md` — 触觉力控对齐

---

### 2.2 数据效率

**现状**: π0.6 通过 RL + Recap 实现了真机自我改进

**空白**:
- 能否在更少数据（<100 episodes）下实现类似效果？
- 合成数据 + 少量真机数据的最佳配比？
- 跨任务的数据复用策略？

**链接**:
- `theory/pi0_6_dissection.md` — Recap 算法
- `theory/vla_rl_practical_guide.md` — VLA + RL 实战

---

### 2.3 边缘部署

**现状**: OpenVLA 支持 QLoRA 4-bit 量化

**空白**:
- 5-10B 参数级别的 VLA 在边缘设备（Orin/Jetson）上的实时推理
- Action Expert 模块的蒸馏压缩
- 精度 vs 速度的最佳平衡点

**链接**:
- `theory/frontier/shallow_pi_knowledge_distillation_flow_vla_2026.md` — 知识蒸馏
- `theory/frontier/qvla_action_centric_quantization_2026.md` — 动作量化

---

## 3. 社区发现的研究空白（来自实战笔记）

### 3.1 GitHub Issues 高价值经验

**来源**: `deployment/community_field_notes_github.md`

| 问题 | 发现 | 机会 |
|------|------|------|
| RTX 50 系列兼容 | GPU 兼容矩阵不完整 | 构建完整兼容性测试 |
| π0 微调陷阱 | 显存优化技巧缺乏文档 | 工程最佳实践总结 |
| GR00T 显存 | 多模态融合显存占用高 | 显存优化方法论 |
| 训练收敛失败 | 根因分析工具缺失 | 自动化诊断工具 |

### 3.2 小红书社区洞察

**来源**: `deployment/community_field_notes_xiaohongshu.md`

> 🔥 社区共识：
> - ACT 50 episodes 就能 work，不需要大数据量
> - Sim2Real 八成是物理参数没校准，不是算法问题
> - 训练成本实测：单卡 A100 约 $X/天

**待研究**:
- 中文社区的硬件选型经验缺乏系统性整理
- 国产机器人（宇树等）的 VLA 适配最佳实践

---

## 4. 跨领域机会

### 4.1 WorldModel × 自动驾驶

**现状**: NVIDIA 在 Physical AI + Autonomous Driving 有大量投入

**机会**:
- 驾驶场景的视频生成作为 world model
- 闭环仿真测试
- 感知-决策联合建模

**链接**: `theory/frontier/nvidia_physical_ai_autonomous_driving_2026.md`

---

### 4.2 WorldModel × 医疗/手术机器人

**空白**: 
- 手术场景的高精度 world model
- 触觉+视觉的联合建模
- 安全关键系统的验证方法

---

### 4.3 多指灵巧手 + VLA

**现状**: Dexterous hand 是 VLA 的难点

**空白**:
- 高自由度动作空间的标准化
- 触觉反馈的融合方式
- 精细操作（如穿针、折叠）的成功率提升

**链接**: 
- `theory/dexterous_hand_mechanics.md`
- `theory/frontier/tacrefinenet_tactile_only_grasp_refinement_2026.md`

---

## 5. 评估体系空白

### 5.1 Benchmark 的局限

**现状**: 
- CALVIN / LIBERO 等 benchmark 覆盖有限
- 真实物理场景的评测成本高

**空白**:
- 长 horizon 任务的评测指标
- 开放世界泛化能力的量化
- Sim2Real transfer gap 的评测

**链接**: 
- `theory/benchmark_tracker.md` — SOTA 追踪
- `theory/evaluation.md` — 评估方法

---

### 5.2 WorldModel 的评测空白

**现状**: WorldArena 试图统一评测，但还不够成熟

**空白**:
- World model 的"功能性"评测（不只是视觉质量）
- Zero-shot 能力的评测方法
- Evaluator accuracy 的标准化

---

### 5.3 Embodied Agent 交互安全评测空白（基于 IS-Bench 深度解析）

**现状**: IS-Bench（AAAI 2026）首次把 embodied safety 从"终局检查"推进为"过程+时序约束"评估

**关键数据**:
- 161 个交互场景、388 个唯一安全风险、10 类家庭风险
- pre-caution（风险前预防）24.2% + post-caution（风险后收尾）75.8%
- **核心发现**：VLM agent "安全完成任务"(SSR) 远低于 "任务完成"(SR)；Safety CoT 提升安全但降低 ~9.4% 任务成功率

**核心洞察**:
1. **安全是时序属性，不是终局属性**：风险不是一开始就在场景里，而是 agent 动作一步步"做出来"的
2. **bbox 比 caption 对安全感知更有用**：安全感知更像 grounded localization 问题，而非语言总结问题
3. **awareness ≠ action**：agent 能识别风险，但不一定能生成对应的 mitigation plan

**研究空白**:
- 如何让 agent 在提升安全性的同时不牺牲任务完成率？（Safety CoT 的效率-安全联合优化）
- pre-caution 特别弱：agent 不擅长在风险发生前主动预防
- 如何将安全约束统一到任务规划框架中，而非事后打补丁？

**链接**: IS-Bench — arXiv:2506.16402 | 项目页: ursulalujun.github.io/isbench.github.io/

---

## 6. 研究路线图建议

### 短期（3-6个月）
1. **边缘部署**: 基于 OpenVLA / UnifolM 的量化压缩研究
2. **Sim2Real**: 物理参数自动校准工具
3. **中文社区**: 国产机器人 VLA 适配最佳实践

### 中期（6-12个月）
4. **WAM**: Video + Action 联合建模的训练稳定性
5. **触觉融合**: 触觉 VLA 的标准化接口
6. **Evaluator**: 通用 policy ranking proxy

### 长期（1-2年）
7. **World Model + RL**: 大规模 World Model RL 训练基础设施
8. **自主 VLA**: 具备自我改进能力的通用机器人基础模型

---

## 7. 关键链接

| 资源 | 链接 |
|------|------|
| WorldModel 主线 | `theory/world_model_mainline.md` |
| VLA 研究主线 | `theory/vla_research_mainline.md` |
| Benchmark 主线 | `theory/frontier/benchmarks/benchmark_mainline.md` |
| GitHub Issues 笔记 | `deployment/community_field_notes_github.md` |
| 小红书中文笔记 | `deployment/community_field_notes_xiaohongshu.md` |
| 真机部署总入口 | `deployment/README.md` |
