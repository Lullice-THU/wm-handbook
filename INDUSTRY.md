# INDUSTRY & COMPANIES — 中国人形机器人行业

> 整理自: [VLA-Handbook](https://github.com/sou350121/VLA-Handbook) 的 companies/ 目录
> 最后更新: 2026-03-30

---

## 中国人形机器人企业估值 TOP10（2026 口径）

> 数据来源: 微信公众号「深蓝具身智能」| 原文口径，不做二次核验

### 榜单总览

| 排名 | 公司 | 城市 | 估值 | 方向/打法 |
|---:|---|---:|---:|---|
| 1 | 优必选（UBTech） | 深圳 | 600 亿+ | 全栈人形：大脑+小脑+本体全自研 |
| 2 | 银河通用（Galbot） | 北京 | 200 亿 | 具身多模态大模型；GraspVLA/GroceryVLA |
| 3 | 智元创新（Agibot） | 上海 | 150 亿 | 多形态通用具身；出货 5100+/市占 39% |
| 4 | 越疆科技（Dobot） | 深圳 | 140 亿+ | 协作机器人+人形；精密操作 |
| 5 | 宇树科技（Unitree） | 杭州 | 120 亿+ | 高性能足式/人形；R1 3.99万起；开源 UnifoLM-VLA-0 |
| 6 | 云深处科技 | 杭州 | 100 亿 | 特种机器人（电力巡检/救援）|
| 7 | 星海图（Galaxea） | 北京 | 100 亿（近） | "先大脑后身体"；EFM-1/RSR/DP3 |
| 8 | 众擎机器人 | 深圳 | — | 高动态运动控制；T800 视频破亿 |
| 9 | 自变量机器人（X Square） | 深圳 | 100 亿 | 端到端通用具身大模型；成立18个月破百亿 |
| 10 | 乐聚智能（Leju） | 深圳 | 90 亿 | 中小型人形+教育科研；市占率 65%+ |

**TOP10 总估值: 1700+ 亿** | 深圳占 5 家（1130 亿+）

### 关键信号
- 2 家已上市，4 家上市辅导中
- 路线高度分化：整机全栈 / 仿真数据 / "大脑优先" / 高动态运动控制

---

## 行业路线分类

| 路线 | 代表公司 | 核心特征 |
|---|---|---|
| 整机全栈 | 优必选 | 大脑+小脑+本体全自研，工业落地叙事 |
| 仿真数据派 | 银河通用 | 十亿级仿真数据，零售场景快速落地 |
| 多形态规模派 | 智元 | 多家族多场景，出货量叙事 |
| 关节/力控积累派 | 越疆 | 协作臂出海→人形精密操作 |
| 足式强产品派 | 宇树 | 四足优势→人形性价比+开源 |
| "大脑优先"派 | 星海图 | 世界模型+算法平台 |
| 高动态运动控制派 | 众擎 | 步态/动态能力作为先导指标 |
| 端到端大模型主义 | 自变量 | WALL-A，端到端终局论 |
| 教育科研平台派 | 乐聚 | 高校合作+教育市场 |

---

## 具身 VLA 面试要点（众擎面经整理）

### 技术面高频题
1. **注意力机制公式** — Scaled Dot-Product Attention，符号写对，说明为何除 √d_k
2. **手撕 Transformer forward** — 最小可执行版本（QKV投影→attention→残差+LN→FFN→残差+LN）
3. **BN vs LN** — 统计维度、优缺点、适用场景
4. **Pre-LN vs Post-LN** — 训练稳定性差异

### 归一化选择原则
- Transformer/VLM/VLA: **LN/RMSNorm**（不依赖batch统计量）
- CNN/batch足够大: **BN**

### 端到端 VLA + RL 路线理解要点
- BC 的局限性: 误差累积、恢复策略、长时程、稀疏奖励
- RL 补充方向: 离线 RL、动作约束、MPC/规则兜底、sim-to-real
- 分层思路: 语义/感知可端到端，控制侧仍需实时约束

---

## 相关文件索引

| 文件 | 说明 |
|---|---|
| `companies/china.md` | 中国公司详情 |
| `companies/asia.md` | 亚洲其他公司 |
| `companies/international.md` | 国际公司 |
| `companies/embodied_ai.md` | 具身AI公司总览 |
| `companies/startups.md` | 初创公司 |
| `question-bank/zhongqing_robotics_embodied_vla_interview_2025.md` | 众擎VLA面经 |
| `question-bank/sharp_robotics_round2_coding_2025.md` | 夏普机器人Coding面经 |
| `question-bank/tencent_roboticsx_embodied_surgery_interview_2026.md` | 腾讯RoboticsX手术机器人面经 |
