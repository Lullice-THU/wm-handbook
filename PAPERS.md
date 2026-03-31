# 重要论文索引

> 整理自: [VLA-Handbook](https://github.com/sou350121/VLA-Handbook) 的 theory/ 目录
> 
> 统计: 193 篇理论文档 | 38 篇 2026 前沿深度解析
> 最后更新: 2026-03-31（新增 Wanderland — 开放世界几何 grounding 仿真平台）

---

## 📊 分类索引

### A. WorldModel 世界模型（核心方向）

#### A1. WorldModel 主线与评测
| 论文 | 方向 | 链接 |
|------|------|------|
| WorldEval | Policy Ranking Evaluator | `theory/frontier/benchmarks/worldeval_world_model_policy_evaluator_2025.md` |
| Ctrl-World × WorldArena | Embodied WM Benchmark | `theory/frontier/benchmarks/ctrl_world_worldarena_embodied_world_model_benchmark_2026.md` |
| **WorldModel 主线总纲** | 演化路径导航 | `theory/world_model_mainline.md` |
| WAM: Three Routes | Video Pretraining 三路线 | `theory/frontier/wam_three_routes_video_pretraining_vs_vla_2026.md` |

#### A2. World Action Model（WAM）
| 论文 | 方向 | 链接 |
|------|------|------|
| **DreamZero** ⭐ | Zero-Shot WAM | `theory/dreamzero_world_action_models_zero_shot_policies_2026.md` |
| World Action Models Are Zero-Shot Policies | WAM 解析 | `theory/world_action_models_are_zero_shot_policies_dissection.md` |
| VLAW | VLA + WM 协同 | `theory/frontier/vlaw_iterative_co_improvement_vla_world_model_2026.md` |
| AtomVLA | Predictive WM + Offline RL | `theory/frontier/atomvla_offline_post_training_predictive_latent_world_models_2026.md` |
| **MIND** ⭐ | WM 记忆一致性 + 动作控制基准 | `theory/frontier/world-model/mind_benchmarking_memory_consistency_and_action_control_in_w_dissection.md` |
| **OLAF** | 潜在动作定向（SeqΔ-REPA 跨场景对齐） | `theory/frontier/world-model/olaf_world_orienting_latent_actions_for_video_world_modeling_dissection.md` |

#### A3. World Model 基础理论
| 论文 | 方向 | 链接 |
|------|------|------|
| GigaBrain | World Model RL Ramp (0.5M Stars) | `theory/gigabrain_0_5m_star_world_model_based_rl_ramp_2026.md` |
| **UCPE** ⭐ | 统一相机位置编码（射线级）| `theory/unified_camera_positional_encoding_for_controlled_video_gene_dissection.md` |
| Causal World Modeling | 因果世界建模 | `theory/causal_world_modeling_for_robot_control_dissection.md` |
| OLAF | World-Orienting Latent Actions | `theory/olaf_world_orienting_latent_actions_for_video_world_modeling_dissection.md` |
| H-WM | Hierarchical WM for TAMP | `theory/h_wm_robotic_task_and_motion_planning_guided_by_hierarchical_dissection.md` |
| Agent World Model Infinity | 合成环境 | `theory/agent_world_model_infinity_synthetic_environments_for_agenti_dissection.md` |
| Causality-Guided Diffusion (CausalGDP) | 因果引导扩散 | `theory/causalgdp_causality_guided_diffusion_policies_for_reinforcem_dissection.md` |

---

### B. VLA 架构与训练

#### B1. 核心架构
| 论文 | 方向 | 链接 |
|------|------|------|
| **VLA 架构总览** | RT-1 → RT-2 → π0 → π0.6 | `theory/vla_arch.md` |
| VLA 研究主线 | 数据规模化→感知增强→RL后训练 | `theory/vla_research_mainline.md` |
| Action Representations | 离散/Diffusion/Flow 三范式 | `theory/action_representations.md` |
| π0 Flow Matching | Flow Matching 原理拆解 | `theory/pi0_flow_matching.md` |
| π0.5 深度解析 | 分层推理 + 开放世界泛化 | `theory/pi0_5_dissection.md` |
| π0.6 深度解析 | RL + Recap + Action Expert | `theory/pi0_6_dissection.md` |

#### B2. 2026 前沿 VLA
| 论文 | 方向 | 链接 |
|------|------|------|
| **VLA-OPD** ⭐ | 反向 KL 桥接 SFT/RL + On-Policy 蒸馏（1-traj 达 87.4% 成功率）| `theory/vla_opd_bridging_offline_sft_and_online_rl_for_vision_langua_dissection.md` |
| **ViFailback** ⭐ | 视觉符号失败诊断 + 外部监督（成功率+22.2%）| `theory/diagnose_correct_and_learn_from_manipulation_failures_via_vi_dissection.md` |
| Figure Helix 0.2 | S1+S2 双系统人形 VLA | `theory/frontier/figure_helix_02_full_body_autonomy_2026.md` |
| SimVLA | 极简 VLA 基线 | `theory/frontier/simvla_simple_vla_baseline_robotic_manipulation_2026.md` |
| ABOT-M0 | 动作流形学习 | `theory/frontier/abot_m0_action_manifold_learning_vla_foundation_2026.md` |
| StarVLA | LEGO-like 模块化架构 | `theory/starvla_lego_like_vla_codebase_2026.md` |
| LingBot | 语言引导 VLA | `theory/lingbot_vla_pragmatic_vla_foundation_model_2026.md` |
| ViTRA | 人类视频预训练 | `theory/frontier/vitra_scalable_vla_pretraining_human_activity_videos_2026.md` |
| Spirit-v1.5 解析 | 端到端代码级理解 | `theory/spirit_v1_5_dissection.md` |
| UnifolM-VLA-0 | 宇树机器人开源训练栈 | `theory/unifolm_vla_0_unitree_2026.md` |
| RDT | 遥感数据 Transformer | `theory/rdt.md` |

#### B3. 经典论文
| 论文 | 方向 | 链接 |
|------|------|------|
| Diffusion Policy | 扩散策略基础 | `theory/diffusion_policy.md` |
| ACT (Action Chunking) | 动作分块 | `theory/act.md` |
| GR00T N1.6 | NVIDIA 机器人基础模型 | `theory/gr00t_n1_6.md` |
| RoboGene | 增强 VLA 预训练 | `theory/robogene_boosting_vla_pre_training_via_diversity_driven_agen_dissection.md` |

---

### C. 触觉与感知

| 论文 | 方向 | 链接 |
|------|------|------|
| TAF-VLA ⭐ | 触觉力控对齐 | `theory/frontier/taf_vla_tactile_force_alignment_2026.md` |
| TacRefineNet | 纯触觉抓取优化 | `theory/frontier/tacrefinenet_tactile_only_grasp_refinement_2026.md` |
| TouchGuide | 推理时触觉引导 | `theory/frontier/touchguide_inference_time_steering_touch_guidance_2026.md` |
| Visual-Tactile Pretraining | 视觉-触觉预训练 | `theory/frontier/visual_tactile_pretraining_online_multitask_learning_2026.md` |
| Tactile-VLA | 触觉 VLA 综述 | `theory/tactile_vla.md` |
| **MSDP** ⭐ | 多感官自监督预训练（6k 交互） | `theory/tactile/self_supervised_multisensory_pretraining_for_contact_rich_ro_dissection.md` |
| Dexterous Hand Mechanics | 灵巧手机械 | `theory/dexterous_hand_mechanics.md` |
| Grasp Algorithms | 抓取算法 | `theory/grasp_algorithms.md` |

---

### D. 强化学习后训练

| 论文 | 方向 | 链接 |
|------|------|------|
| **VLA-OPD** ⭐ | 反向 KL 桥接 SFT/RL + On-Policy 蒸馏 | `theory/vla_opd_bridging_offline_sft_and_online_rl_for_vision_langua_dissection.md` |
| GigaBrain | World Model RL (0.5M Stars) | `theory/gigabrain_0_5m_star_world_model_based_rl_ramp_2026.md` |
| Evo-RL | 真机 RL 闭环 | `theory/frontier/evo_rl_open_real_world_rl_recap_pistar06_so101_2026.md` |
| VLA RL Practical Guide | VLA + RL 实战 | `theory/vla_rl_practical_guide.md` |
| Reinforcement Learning | RL 基础理论 | `theory/reinforcement_learning.md` |
| GR-RL | Goal-conditioned RL | `theory/gr_rl_dissection.md` |
| π0-StepNFT | 在线 RL 步长 | `theory/pi_stepnft_wider_space_needs_finer_steps_in_online_rl_for_fl_dissection.md` |
| VLGOR | Visual Language Guided Offline RL | `theory/vlgor_visual_language_knowledge_guided_offline_reinforcement_dissection.md` |
| Scaling Verification | 验证规模化 | `theory/scaling_verification_can_be_more_effective_than_scaling_poli_dissection.md` |
| Lifelong Imitation Learning | 终身模仿学习 | `theory/lifelong_imitation_learning_with_multimodal_latent_replay_an_dissection.md` |

---

### E. 效率与部署

| 论文 | 方向 | 链接 |
|------|------|------|
| Shallow-Pi ⭐ | VLA 知识蒸馏 | `theory/frontier/shallow_pi_knowledge_distillation_flow_vla_2026.md` |
| QVLA | 动作中心化量化 | `theory/frontier/qvla_action_centric_quantization_2026.md` |
| RDT2-UMI | 跨具身零样本 | `theory/frontier/rdt2_umi_zero_shot_cross_embodiment_2026.md` |
| RoboPocket | 手机端策略迭代 | `theory/frontier/robopocket_robot_free_instant_policy_iteration_phone_2026.md` |
| Small VLA Models | 小型化 VLA | `theory/small_vla_models.md` |
| Knowledge Distillation | 知识蒸馏理论 | `theory/knowledge_distillation.md` |
| Quantization Theory | 量化理论 | `theory/quantization_theory.md` |
| PEFT/LoRA | 参数高效微调 | `theory/peft_lora.md` |
| DoRA | 权重分解 LoRA | `theory/dora_weight_decomposed_low_rank_adaptation.md` |
| KV Cache / LLM Inference | 推理优化 | `theory/kv_cache_llm_inference.md` |
| Flash Attention | 注意力优化 | `theory/flash_attention.md` |

---

### F. 视觉与推理

| 论文 | 方向 | 链接 |
|------|------|------|
| Thinker-VLM | Embodied VLM | `theory/frontier/thinker_vlm_embodied_visual_language_model_2026.md` |
| Multimodal Models | 多模态模型基础 | `theory/multimodal_models.md` |
| Chain of Thought | 思维链 | `theory/chain_of_thought.md` |
| LangGap | 语言鸿沟诊断 | `theory/langelog_diagnosing_and_closing_the_language_gap_in_vision_la_dissection.md` |
| Perception Techniques | 感知技术 | `theory/perception_techniques.md` |

---

### G. 数据与 Sim2Real

| 论文 | 方向 | 链接 |
|------|------|------|
| **Wanderland** ⭐ | 开放世界几何 grounding 仿真平台（LiDAR+IMU+RGB 多传感器融合 + LIV-SLAM，metric-scale 几何）| `theory/wanderland_geometrically_grounded_simulation_for_open_world_dissection.md` |
| Data for VLA | 数据集综述 | `theory/data.md` |
| Self-Supervised Learning | 自监督学习 | `theory/self_supervised_learning.md` |
| Isaac Lab | 仿真平台 | `theory/isaac_lab.md` |
| Co-training | 协同训练 | `theory/co_training.md` |
| Transfer Learning | 迁移学习 | `theory/transfer_learning.md` |
| Robot Dynamics Classification | 机器人动力学分类 | `theory/robot_dynamics_classification.md` |
| State Estimation | 状态估计 | `theory/state_estimation.md` |
| Pointcloud SLAM | 点云 SLAM | `theory/pointcloud_slam.md` |

---

### H. 评估与 Benchmark

| 论文 | 方向 | 链接 |
|------|------|------|
| Benchmark 主线 | 评估体系导航 | `theory/frontier/benchmarks/benchmark_mainline.md` |
| Evaluation | 评估方法 | `theory/evaluation.md` |
| Benchmark Tracker | SOTA 追踪 | `theory/benchmark_tracker.md` |
| TACO | 视频编解码 | `theory/taco_a_benchmark_for_lossless_and_lossy_codecs_of_heterogene_dissection.md` |
| **BeSafe-Bench** ⭐ | 四域行为安全基准（Web/Mobile/Embodied VLM/VLA，1312任务/9类风险/S-S联合评估） | `theory/frontier/benchmarks/besafe_bench_unveiling_behavioral_safety_risks_of_situated_a_dissection.md` |
| MIND | WM 记忆一致性 + 动作控制基准（250段1080p视频/5维指标） | `theory/frontier/world-model/mind_benchmarking_memory_consistency_and_action_control_in_w_dissection.md` |
| ENACT | Embodied Cognition + Egocentric WM | `theory/frontier/benchmarks/enact_embodied_cognition_world_modeling_egocentric_interaction_2025.md` |

---

### I. 安全与对齐

| 论文 | 方向 | 链接 |
|------|------|------|
| Alignment VLA | VLA 对齐 | `theory/alignment_vla.md` |
| Concept-Based Dictionary | 推理时安全 | `theory/concept_based_dictionary_learning_for_inference_time_safety_dissection.md` |
| When to Act/Ask/Learn | 不确定性感知策略 | `theory/when_to_act_ask_or_learn_uncertainty_aware_policy_steering_dissection.md` |
| **IS-Bench** ⭐ | VLM Embodied Agent 交互安全评估（161场景/388风险/10类家庭风险/过程导向评估） | `theory/frontier/benchmarks/is_bench_interactive_safety_vlm_embodied_agents_household_tasks_2025.md` |
| VLA Intrinsic Safety | VLA 内在安全性 | `theory/frontier/vla_intrinsic_safety.md` |

---

### J. NVIDIA 与 Infra

| 论文 | 方向 | 链接 |
|------|------|------|
| NVIDIA Physical AI | 物理 AI | `theory/frontier/nvidia_physical_ai_autonomous_driving_2026.md` |
| NVIDIA AI 5-Layer Cake | 基建架构 | `theory/frontier/nvidia_ai_5_layer_cake_infrastructure_2026.md` |
| PI Robot API | Physical Intelligence Layer | `theory/frontier/physical_intelligence_layer_robot_api_2026.md` |
| RynnBrain | 开源基础模型 | `theory/frontier/rynnbrain_open_embodied_foundation_models_2026.md` |
| WALL-OSS | 开源 VLA | `theory/wall_oss.md` |

---

### K. 其他专题

| 论文 | 方向 | 链接 |
|------|------|------|
| VideoWeaver | 多视角视频迁移 | `theory/videoweaver_multimodal_multi_view_video_to_video_transfer_fo_dissection.md` |
| Uni-Skill | 自进化技能库 | `theory/uni_skill_building_self_evolving_skill_repository_for_genera_dissection.md` |
| FAVLA | 力适应 VLA | `theory/favla_a_force_adaptive_fast_slow_vla_model_for_contact_rich_dissection.md` |
| TwinVLA | 双臂操作 | `theory/twinvla_data_efficient_bimanual_manipulation_with_twin_singl_dissection.md` |
| Equibim | 双臂对称等变 | `theory/equibim_learning_symmetry_equivariant_policy_for_bimanual_ma_dissection.md` |
| Contractive Diffusion | 鲁棒扩散 | `theory/contractive_diffusion_policies_robust_action_diffusion_via_c_dissection.md` |
| Mind Benchmarking | 记忆一致性 | `theory/mind_benchmarking_memory_consistency_and_action_control_in_w_dissection.md` |
| Neural Implicit Action Fields | 隐式动作场 | `theory/neural_implicit_action_fields_from_discrete_waypoints_to_con_dissection.md` |
| Characterizing VLA | VLA 特性分析 | `theory/characterizing_vla_models_identifying_the_action_generation_dissection.md` |
| Closed-Loop Action Chunks | 动态校正闭环 | `theory/closed_loop_action_chunks_with_dynamic_corrections_for_train_dissection.md` |
| Beyond Attention Magnitude | 层间 rank 分析 | `theory/beyond_attention_magnitude_leveraging_inter_layer_rank_consi_dissection.md` |

---

## 🎯 按推荐阅读排序

### 入门路线（30分钟）

1. `theory/vla_arch.md` (5min) — VLA 核心架构
2. `theory/action_representations.md` (10min) — 动作生成三范式
3. `theory/pi0_flow_matching.md` (10min) — Flow Matching 原理
4. `theory/world_model_mainline.md` (5min) — ⭐ WorldModel 主线

### WorldModel 专项

1. `theory/world_model_mainline.md` — 主线导航
2. `theory/dreamzero_world_action_models_zero_shot_policies_2026.md` — DreamZero
3. `theory/frontier/wam_three_routes_video_pretraining_vs_vla_2026.md` — WAM 三路线
4. `theory/gigabrain_0_5m_star_world_model_based_rl_ramp_2026.md` — GigaBrain
5. `theory/causal_world_modeling_for_robot_control_dissection.md` — 因果 WM

### VLA 架构专项

1. `theory/vla_arch.md` — 架构总览
2. `theory/pi0_5_dissection.md` — π0.5
3. `theory/pi0_6_dissection.md` — π0.6
4. `theory/frontier/figure_helix_02_full_body_autonomy_2026.md` — Figure Helix

### 工程部署专项

1. `theory/unifolm_vla_0_unitree_2026.md` — 开源训练栈
2. `theory/frontier/shallow_pi_knowledge_distillation_flow_vla_2026.md` — 知识蒸馏
3. `theory/deployment/README.md` — 真机部署总入口
