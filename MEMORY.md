# MEMORY.md — WM Research OPC

> Last Updated: 2026-04-01 03:00 (OPC-WM subagent assessment)

## 项目状态

- **阶段**: Phase 1 评估完成，Phase 2 规划中
- **目录**: `~/.openclaw/workspace/opc/wm-research/`
- **GitHub**: 未上传（yellow/wm-research 404，等 Yellow 提供 Token）
- **Token 需求**: GitHub Personal Access Token（repo 权限）

---

## Phase 1 完成度评估（2026-03-24 → 2026-04-01）

### ✅ 已完成（超额完成）

| 指标 | 目标 | 实际 | 状态 |
|------|------|------|------|
| MD 文件数 | ~24 | **34** | ✅ 超额 |
| 深度解析 | 7篇 | **5+2** | ✅ |
| 论文索引 | 193篇 | **193篇** | ✅ |
| Companies 文档 | 6家 | **6家**（PI, Figure, 1X, DeepMind, Tesla, Megan） | ✅ |
| 周报 | 1期 | **1期**（2026-03-31） | ✅ |
| 差距分析 | - | **WM_VS_VLA_GAP_ANALYSIS.md**（320行） | ✅ |
| 基础设施 | - | CLAUDE.md, CONTRIBUTING.md, CHANGELOG.md, AGENTS.md, SOUL.md | ✅ |

### ⚠️ 部分完成 / 未完成

| 指标 | 状态 | 说明 |
|------|------|------|
| GitHub 上传 | ❌ 未完成 | 等 Yellow 提供 Token |
| memory/ 目录 | ❌ 未创建 | 尚未建立 blog/archives 结构 |
| docs/biweekly/ | ⚠️ 空目录 | 仅有占位 README，无实际报告 |
| docs/theory/ | ⚠️ 仅1篇 | DREAMZERO_DEEP_DIVE.md |
| docs/weekly/ | ⚠️ 仅1期 | 需建立每周更新节奏 |
| 自动化 Pipeline | ❌ 未建立 | VLA-Handbook 每日 Commit 脚本缺失 |
| 社区笔记采集 | ❌ 未建立 | social intelligence 跟踪机制缺失 |

### 📁 关键文件路径

```
wm-research/
├── MEMORY.md          ← 本文件
├── SOUL.md            ← OPC 行为宪法
├── AGENTS.md          ← 协作规范
├── README.md          ← 项目入口
├── WORLDMODEL_OVERVIEW.md   ← 核心主线
├── VLA_ARCHITECTURE.md      ← VLA 架构
├── PAPERS.md          ← 论文索引（193篇）
├── RESEARCH_GAPS.md   ← 研究空白
├── INDUSTRY.md        ← 行业概览
├── CLAUDE.md          ← AI 协作规范
├── CONTRIBUTING.md    ← 贡献指南
├── CHANGELOG.md       ← 变更记录
├── CODE_EXAMPLES.md   ← 代码示例
│
├── theory/            ← 深度理论解析
│   ├── DREAMZERO.md   ⭐ WAM 核心
│   ├── WORLDEVAL.md   ⭐ Policy Evaluator
│   ├── MIND.md        ⭐ 长程记忆一致性
│   ├── README.md
│   └── frontier/
│       ├── ATOMVLA.md
│       └── benchmarks/
│           └── BeSafeBench.md
│
├── docs/
│   ├── WEEKLY_PROGRESS_2026_03_31.md   ← 第1期周报
│   ├── WM_VS_VLA_GAP_ANALYSIS.md       ← 差距分析
│   ├── weekly/              ← 周报存档（空）
│   ├── biweekly/            ← 双周报（空）
│   └── theory/              ← 理论文档（仅1篇）
│
├── cheat-sheet/
│   └── companies/           ← 6家公司档案
│       ├── 1X_Technologies.md
│       ├── Physical_Intelligence.md
│       ├── Figure_AI.md
│       ├── DeepMind.md
│       ├── Tesla_Optimus.md
│       ├── Megan_ByteDance.md
│       └── README.md
│
└── question-bank/
    └── INTERVIEW_WM.md
```

---

## Phase 2 优先任务（2026-04-01 起）

### 🔴 P0 — 阻塞级（等 Yellow 配合）

1. **GitHub 上传** — 等 Yellow 提供 Personal Access Token
   - 动作：收到 Token → `gh repo create yellow/wm-research --public --clone` → git push
   - 替代方案：手动告知 Yellow `git remote add origin https://github.com/yellow/wm-research.git`

### 🟡 P1 — 高优先级（可立即开始）

2. **建立 memory/ 目录结构**
   ```bash
   memory/
   ├── blog/
   │   └── archives/     # VLA 社交情报存档
   ├── daily/            # 日志
   └── domains/          # 领域知识
   ```

3. **建立自动化 Pipeline（VLA-Handbook 跟踪）**
   - 每周日：从 VLA-Handbook GitHub API 拉取最新 commit
   - 评分：新论文 → ⚡/🔧/📖/❌
   - 输出：更新 PAPERS.md + 新增 theory/ 文件 + 周报

4. **docs/biweekly/ 建立双周报告模板**
   - 格式：对标 WEEKLY_PROGRESS_2026_03_31.md
   - 频率：每两周一次

### 🟢 P2 — 中优先级

5. **docs/theory/ 扩充**
   - 优先补全：VLA-Handbook 高价值页面 → 本地理论文档
   - 目标：2026-04-15 前再增加 3-5 篇深度解析

6. **companies/ 更新**
   - 1X Technologies: 补充 2026年 Neo Beta 最新进展
   - Megan: 补充 ByteDance 内部 WM 进展
   - DeepMind: 补充 RT-2X / RT-3 最新动态

7. **docs/weekly/ 每周节奏建立**
   - 每周日生成周报（自动或手动）
   - 周报内容：新论文 + 趋势分析 + 研究空白更新

---

## 核心假设追踪

| # | 假设 | 置信度 | 最后验证 |
|---|------|--------|---------|
| 1 | VLA 安全对齐是 2026 年落地关键 | 高 | 2026-03-31 |
| 2 | 反向 KL 将成为 SFT→RL 桥接主流 | 中 | 2026-03-31 |
| 3 | WM 长程一致性是最难解决的瓶颈 | 高 | 2026-03-31 |
| 4 | 安全对齐 > 后训练效率 > 长程一致性（优先级排序）| 中 | 2026-03-31 |

---

## 研究空白优先级（Research Gaps）

| 优先级 | 空白 | 说明 |
|--------|------|------|
| 🥇 P1 | Evaluator 稳定性 | WorldEval ranking proxy 大规模验证缺失 |
| 🥇 P1 | WM 记忆一致性 | MIND: >50帧显著衰减，环路误差累积 |
| 🥈 P2 | 安全对齐机制 | BeSafe-Bench: 41%成功任务伴随安全风险 |
| 🥈 P2 | SFT→RL 桥接效率 | VLA-OPD 反向KL，但泛化性待验证 |
| 🥉 P3 | 几何 grounding | 开放世界穿模、物体关系错误 |
| 🥉 P3 | 多域统一评估 | BeSafe-Bench 四域基准仍属早期 |

---

## 研究趋势（2026-03-31 周报总结）

| 趋势 | 置信度 |
|------|--------|
| 安全先行：S-U 问题受到前所未有重视 | ⭐⭐⭐ |
| 后训练效率：少样本离线数据驱动 VLA 后训练 | ⭐⭐⭐ |
| 多域统一评估：Web+Mobile+Embodied+VLA 四域 | ⭐⭐⭐ |
| 连续动作建模：离散→连续潜在动作 | ⭐⭐ |
| 几何 grounding：开放世界仿真核心瓶颈 | ⭐⭐ |

---

## 数据来源

- VLA-Handbook: https://github.com/sou350121/VLA-Handbook
- 每周日自动检查更新（待 Pipeline 建立）

---
_更新: 2026-04-01 03:00 by OPC-WM subagent_
