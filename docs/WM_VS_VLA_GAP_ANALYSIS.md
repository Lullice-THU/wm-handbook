# WorldModel Handbook vs VLA Handbook — 差距分析报告

**报告日期:** 2026-03-31
**分析目的:** 识别 WM 项目达到 VLA Handbook 权威水平所需的差距
**数据来源:** VLA-Handbook README + GitHub 仓库结构 + WM 项目本地文件

---

## 📊 一、整体差距概览

| 维度 | VLA Handbook | WM 项目 | 差距 |
|------|-------------|---------|------|
| **仓库规模** | 684 Commits / 107 Stars | ~10 Commits | ⚠️ 严重不足 |
| **核心文档** | 186 篇理论文档 | 9 篇文档（~65KB） | ⚠️ 差 20× |
| **前沿解析** | 33 篇 2026 深度解析 | 0 篇 | ❌ 空白 |
| **社区笔记** | 📕 300+ / 📘 165 / 🔧 47 条 | 0 条 | ❌ 空白 |
| **周报** | 29 期 + 12 期双周报告 | 0 期 | ❌ 空白 |
| **自动化 Pipeline** | 33 个 Cron Job | 0 个 | ❌ 空白 |
| **脚本系统** | SCRIPTS.md 含完整 DAG | 无 | ❌ 空白 |
| **面试题库** | 15 份 | 无 | ❌ 空白 |
| **公司分析** | 12 份 | 无 | ❌ 空白 |
| **速查表** | cheat-sheet/ | 无 | ❌ 空白 |
| **电子书** | book/ | 无 | ❌ 空白 |
| **Agent 系统** | adversarial-research-analyst/ | 无 | ❌ 空白 |
| **CLAUDE.md** | 有（跨会话记忆系统） | 无 | ❌ 空白 |
| **基础设施** | CONTRIBUTING + CHANGELOG + LICENSE | 无 | ❌ 空白 |
| **活跃度** | 每日多次 commit | 不定期 | ⚠️ 差距大 |

---

## 📁 二、文档结构对比

### VLA Handbook 完整目录结构

```
VLA-Handbook/
├── theory/                          # 186 篇理论文档
│   ├── README.md                     # 路线图 + 核心概念索引
│   ├── paper_index.md                # 多维索引 + 发展史全景图
│   ├── world_model_mainline.md        # ⭐ WorldModel 主线导航
│   ├── vla_arch.md                   # RT-1/2 → π0 演进
│   ├── vla_research_mainline.md       # 研究主线
│   ├── action_representations.md      # 离散/Diffusion/Flow
│   ├── evaluation.md                  # 评估方法
│   ├── benchmark_tracker.md           # SOTA 追踪
│   ├── frontier/                      # 前沿论文目录
│   │   ├── benchmarks/               # 评测基准
│   │   ├── world-model/              # WorldModel 专项
│   │   └── ...
│   └── [160+ 深度解析文档]
├── deployment/                        # 真机部署
│   ├── README.md                     # 硬件选型 · 多模态同步 · Sim2Real
│   ├── community_field_notes_xiaohongshu.md  # 📕 300+ 条中文笔记
│   ├── community_field_notes_english.md       # 📘 165 条英文笔记
│   └── community_field_notes_github.md        # 🔧 47 条 GitHub Issues
├── reports/
│   ├── weekly/                       # 29 期周报 + 每日 digest
│   └── biweekly/                     # 12 期双周推理报告（带预测回顾）
├── memory/blog/archives/
│   └── vla-social-intel/             # 30 期社交情报 + 原始数据
├── scripts/                           # 自动化 Pipeline（SCRIPTS.md 含 DAG）
├── question-bank/                    # 15 份面试题库与代码实战
├── companies/                        # 12 份机器人公司分析
├── cheat-sheet/                      # 速查表（时间线 · 核心公式）
├── book/                             # 电子书版本
├── adversarial-research-analyst/     # VLA 专家系统（docs + reports + skill + XHS）
├── system-design/                    # 系统设计
├── product/                          # 产品设计
├── docs/                             # 文档
├── assets/                           # 资源文件
├── AGENTS.md (Symlink)              # Agent 协作规范
├── CLAUDE.md                         # 跨会话记忆系统
├── CONTRIBUTING.md                   # 贡献指南
├── CHANGELOG.md                      # 变更记录
├── LICENSE (CC BY 4.0)              # 许可证
└── collected_urls.json               # URL 数据库
```

### WM 项目当前结构

```
wm-research/
├── WORLDMODEL_OVERVIEW.md           # WorldModel 技术主线 ✅
├── VLA_ARCHITECTURE.md              # VLA 架构（部分内容）
├── PAPERS.md                        # 论文索引 (~14KB) ✅
├── CODE_EXAMPLES.md                 # 代码示例 (~7KB) ✅
├── RESEARCH_GAPS.md                  # 研究空白 (~9KB) ✅
├── INDUSTRY.md                       # 行业信息 (~4KB) ✅
├── README.md                        # 项目入口 ✅
├── MEMORY.md                        # 记忆文件 ✅
├── SOUL.md                          # 行为宪法 ✅
├── HEARTBEAT.md                     # 心跳配置 ✅
└── docs/
    ├── WEEKLY_PROGRESS_2026_03_31.md # 周报 ✅（刚生成）
    └── (其他文档)
```

---

## 🔬 三、内容深度对比

### 3.1 理论文档质量

| 指标 | VLA | WM | 差距 |
|------|-----|-----|------|
| 论文覆盖数 | 186 篇 | ~40 篇 | ⚠️ 不足 5× |
| 2026 前沿解析 | 33 篇 | 0 篇 | ❌ 无 |
| 深度拆解文档 | 完整（含代码/超参/sanity-check） | 摘要级 | ⚠️ 差距大 |
| 工程细节 | 入口脚本/关键超参/shape 校验 | 缺失 | ❌ 无 |
| 引用链接 | 完整原文链接 | 部分 | ⚠️ 待完善 |

### 3.2 社区内容

VLA 有三份独特的社区实战笔记，这是**最核心的差异化内容**：

| 来源 | 内容 | WM 有无 |
|------|------|--------|
| 📕 小红书中文 | 300+ 条中文社区蒸馏（训练成本/真实参数/失败复盘） | ❌ 无 |
| 📘 英文社区 | 165 篇 HF Blog + Discord + 厂商博客精选 | ❌ 无 |
| 🔧 GitHub Issues | 6 大仓库 47 条高互动 Issues（GPU 兼容/显存优化） | ❌ 无 |

**这是 VLA Handbook 最独特的价值**——"论文不会告诉你的事"都在社区笔记里。

### 3.3 报告体系

| 报告类型 | VLA | WM |
|---------|-----|-----|
| 周报 | 29 期存档 | 1 期（刚生成） |
| 双周推理报告 | 12 期（含预测回顾 ✅/❌） | ❌ 无 |
| 每日社交情报 | 30 期存档 | ❌ 无 |
| 每日论文评分 | ⚡/🔧/📖/❌ 评级 | ❌ 无 |
| 月度趋势分析 | 有 | ❌ 无 |

---

## ⚙️ 四、基础设施对比

### 4.1 自动化 Pipeline

**VLA 的自动化系统（Pulsar）：**
- 33 个 Cron Job，每日全自动运行
- ⚡ 论文评分（每日 09:15）：30+ 篇/天 → ⚡/🔧/📖/❌ 精选
- 🛰️ 社交情报（每日 09:30）
- 🔬 深度解析（一/三/五 15:30）
- 📕 小红书增量（每 3 天）
- 📘 英文社区（每周五）
- 📋 周报（每周日）
- 📊 双周报告（每两周）
- 自我进化系统：维护 19 条领域假设 + 置信度分数 + 自动调整
- 自愈 Watchdog：23 项健康检查

**WM 当前状态：**
- 0 个 Cron Job
- 只有 OPC Agent 心跳（每 10 分钟检查仓库）
- 无自动化论文评分
- 无社区内容采集
- 无自我进化机制

### 4.2 Agent 系统

**VLA 有完整的 Agent 系统：**
- `adversarial-research-analyst/` — 对抗性研究分析师
  - docs/ — VLA 专家系统文档
  - reports/ — 报告
  - skill files — 即插即用的 AI Skill
  - xiaohongshu collector — 小红书采集器
- `AGENTS.md` — Agent 协作规范
- `CLAUDE.md` — 跨会话记忆系统
- VLA Expert Skill — 可在 Claude Code/Cursor/Codex 上使用

**WM 当前状态：**
- 只有基础的 OPC Agent（子修 + OPC-WM）
- 无专业研究 Agent
- 无即插即用的 AI Skill

### 4.3 工程系统

| 系统 | VLA | WM |
|------|-----|-----|
| 版本变更记录 | CHANGELOG.md | ❌ 无 |
| 贡献指南 | CONTRIBUTING.md | ❌ 无 |
| 许可证 | CC BY 4.0 | ❌ 无 |
| URL 数据库 | collected_urls.json | ❌ 无 |
| 速查表 | cheat-sheet/ | ❌ 无 |
| 面试题库 | question-bank/（15份） | ❌ 无 |
| 公司分析 | companies/（12份） | ❌ 无 |
| 电子书 | book/ | ❌ 无 |

---

## 📈 五、社区活跃度对比

| 指标 | VLA Handbook | WM 项目 |
|------|-------------|---------|
| Stars | 107 | — |
| Forks | 5 | — |
| Commits | 684 | ~10 |
| 贡献者 | 3（人 + AI Agent） | 1 |
| 最近 commit | 3 小时前 | 数小时前 |
| 日均 commit | 2-5 个 | 0-1 个 |
| Issues | 1 | — |
| 自动化更新 | 33 个 Cron Job | 0 |

---

## 🎯 六、关键差距总结（按优先级）

### 🔴 P0 — 核心差距（无替代方案）

| 差距 | 影响 | 建议 |
|------|------|------|
| **无理论深度解析文档** | 无法建立领域权威性 | 每篇论文需要"解剖级"解析，而非摘要 |
| **无社区实战笔记** | 失去"论文不会告诉你的事"这个最大差异化价值 | 必须建立中文/英文社区采集机制 |
| **无自动化 Pipeline** | 内容无法自动更新，变成静态文档 | 需要类似 Pulsar 的自动采集 + 评分系统 |
| **无周报/双周报告体系** | 无法持续跟踪领域进展 | 建立每周日报 + 双周趋势预测 |
| **无研究空白分析体系** | 无法为研究者提供明确的机会点 | 需要类似 RESEARCH_GAPS.md 的持续更新版 |

### 🟡 P1 — 重要差距（需要建设）

| 差距 | 影响 | 建议 |
|------|------|------|
| **论文覆盖数不足** | 目录看起来单薄 | 扩展到 100+ 篇（尤其 WorldModel 专项） |
| **无面试题库** | 失去"刷面试"这个强需求用户群 | 建立 5-10 份面试题 |
| **无速查表** | 缺少快速入口 | 建立 cheat-sheet/ 时间线 + 核心公式 |
| **无公司/求职分析** | 失去产业视角读者 | 建立 companies/ 目录 |
| **无 CLAUDE.md/AGENTS.md** | Agent 间协作缺乏规范 | 参考 VLA 编写 |

### 🟢 P2 — 锦上添花（后期建设）

| 差距 | 建议 |
|------|------|
| 电子书版本 (book/) | 后期考虑 |
| AI Expert Skill | 后期考虑（类似 VLA Expert Skill） |
| 自我进化系统 | 长期目标 |

---

## 🗺️ 七、追赶路线建议（⚡ 7×24 Agent驱动版）

> ⚠️ **重大调整：** Yellow 指示 OPC 是 AI Agent 驱动，7×24 小时不间断工作，时间表激进 5-10 倍。
> - Agent 不睡觉，不需要休息
> - Central Dispatcher 每 15 分钟派发任务
> - 可并行处理多个子任务
> - 持续监控，无需人工干预

### 阶段 1 — 短期（1-3 天）：🔥 极速建立基础

| # | 任务 | 状态 | 负责人 |
|---|------|------|--------|
| 1.1 | **扩展 PAPERS.md** 到 80+ 篇（重点补 WorldModel 专项） | 🔄 进行中 | Agent |
| 1.2 | **建立 RESEARCH_GAPS 自动更新机制**（Cron 每 2 天） | ⬜ | Agent |
| 1.3 | **生成第一篇深度解析**（DreamZero / OLAF 二选一） | ⬜ | Agent |
| 1.4 | **补充 CLAUDE.md + CONTRIBUTING.md** | ⬜ | Agent |

**理由：** 原 1-2 周 → 现 1-3 天。Agent 并行处理多个文档更新，24 小时持续工作。

### 阶段 2 — 中期（1-2 周）：⚡ 内容极速丰富

| # | 任务 | 状态 |
|---|------|------|
| 2.1 | **达到 30 篇深度解析**（目标：2026 前沿全覆盖） | ⬜ |
| 2.2 | **建立自动周报机制**（Cron 每周日 + 每日简报） | ⬜ |
| 2.3 | **建立社区笔记采集**（小红书 + GitHub Issues） | ⬜ |
| 2.4 | **补充面试题库**（5 份 + 速查表） | ⬜ |

**理由：** 原 1 个月 → 现 1-2 周。多 Agent 并行研究，Central Dispatcher 持续派发。

### 阶段 3 — 长期（1-2 个月）：🎯 权威化 + VLA Handbook 同等规模

| # | 任务 | 状态 |
|---|------|------|
| 3.1 | **建立自动化 Pipeline**（类似 Pulsar 的论文评分 + 采集系统） | ⬜ |
| 3.2 | **达到 100 篇理论文档**（186 篇 VLA - WM 差距弥合） | ⬜ |
| 3.3 | **建立双周趋势预测报告** | ⬜ |
| 3.4 | **补充速查表 + 公司分析 + AGENTS.md** | ⬜ |
| 3.5 | **达到 VLA Handbook 同等权威性**（186 篇 + 38 篇 2026 前沿） | ⬜ |
| 3.6 | **建立自我进化机制**（假设检验 + 置信度追踪） | ⬜ |
| 3.7 | **发布 WM Expert Skill** | ⬜ |
| 3.8 | **Stars 目标：30+** | ⬜ |

**理由：** 原 6 个月 → 现 1-2 个月。7×24 不间断工作，持续 commit，接近 VLA 的每日活跃度。

---

### 📊 时间线对比

| 阶段 | 原计划 | ⚡ Agent驱动 | 压缩比 |
|------|--------|-------------|--------|
| 短期 | 1-2 周 | **1-3 天** | ~5× |
| 中期 | 1 个月 | **1-2 周** | ~3× |
| 长期 | 6 个月+ | **1-2 个月** | ~3-5× |

---

## 📎 八、附录

### VLA Handbook 关键链接
- 仓库：https://github.com/sou350121/VLA-Handbook
- 自动化系统：https://github.com/sou350121/Pulsar-KenVersion
- VLA Expert Skill：https://github.com/sou350121/VLA-expert-skill

### WM 项目当前文件清单
```
PAPERS.md (14KB) - 论文索引
WORLDMODEL_OVERVIEW.md (11KB) - WorldModel 技术主线
VLA_ARCHITECTURE.md (11KB) - VLA 架构
RESEARCH_GAPS.md (9KB) - 研究空白
CODE_EXAMPLES.md (7KB) - 代码示例
INDUSTRY.md (4KB) - 行业信息
README.md (4KB) - 项目入口
MEMORY.md (23KB) - 记忆文件
SOUL.md (1KB) - 行为宪法
HEARTBEAT.md (1KB) - 心跳配置
docs/WEEKLY_PROGRESS_2026_03_31.md (5KB) - 周报
```

---

*报告生成：OPC wm-research Agent*
*数据来源：VLA-Handbook GitHub + 本地 WM 项目文件*
