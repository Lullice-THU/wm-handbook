# CLAUDE.md — WorldModel Handbook AI 协作规范

> 本文件定义了 WorldModel Handbook 的 AI Agent 协作规范。
> 所有参与本项目的 Agent 必须遵循此规范。

---

## 🤖 Agent 架构

### 角色定义

| Agent | 职责 | 权限边界 |
|-------|------|---------|
| **子修（Main）** | 调度、汇报、维护 Yellow 上下文 | OPC 调度中心 |
| **OPC-WM** | WorldModel 调研、论文分析、知识库维护 | 仅 wm-research 目录 |
| **WM-Build** | 知识库建设、内容扩展 | 仅 wm-research 目录 |

### 记忆隔离原则

- 每个 Agent 有**独立的 memory namespace**
- OPC-WM 与 WM-Build 之间**通过文件交换数据**
- 所有 Agent 共享 `MEMORY.md` 作为状态同步

---

## 📋 任务执行规范

### 论文分析流程

1. **抓取** — 从 VLA-Handbook GitHub 获取新论文
2. **评级** — ⚡ 重要 / 🔧 工程可用 / 📖 值得了解 / ❌ 跳过
3. **解析** — 生成深度解析文档（代码级 + 工程细节）
4. **索引** — 更新 PAPERS.md
5. **记录** — 更新 MEMORY.md

### 文档更新规范

- **PAPERS.md**：每次新增论文必须同步更新
- **MEMORY.md**：每次心跳前必须更新进展
- **CHANGELOG.md**：每次内容变更必须记录

---

## 🔄 跨会话状态同步

### 通过文件系统同步

```
~/.openclaw/workspace/opc/wm-research/
├── MEMORY.md      ← 跨会话状态（每个 Agent 必须读写）
├── HEARTBEAT.md   ← 心跳配置
└── docs/          ← 报告输出目录
```

### MEMORY.md 必须包含

- 最新 commit 信息
- 当前进行中的任务
- 待 Yellow 决策事项
- 已完成任务清单

---

## 📊 自我进化机制

### 领域假设追踪

维护以下核心假设，标注置信度：

| # | 假设 | 置信度 | 最后验证 |
|---|------|--------|---------|
| 1 | VLA 安全对齐是 2026 年落地关键 | 高 | 2026-03-31 |
| 2 | 反向 KL 将成为 SFT→RL 桥接主流 | 中 | 2026-03-31 |
| 3 | WM 长程一致性是最难解决的瓶颈 | 高 | 2026-03-31 |

### 假设更新规则

- 新论文支持 → 置信度提升
- 反面证据 → 置信度下降
- 长期无验证 → 标记 watch-list

---

## 🗂️ 目录结构规范

```
~/.openclaw/workspace/opc/wm-research/
├── theory/              # 理论文档（深度解析）
├── deployment/          # 部署相关
├── reports/
│   ├── weekly/         # 周报
│   └── biweekly/       # 双周报告
├── memory/
│   └── blog/
│       └── archives/   # 社交情报存档
├── scripts/             # 自动化脚本
├── cheat-sheet/         # 速查表
└── companies/          # 公司分析
```

---

## ⚡ 紧急情况处理

### 发现关键论文（⚡ 评级）

1. 立即更新 MEMORY.md
2. 生成深度解析（优先级 P0）
3. 向子修汇报

### 发现系统性问题

1. 记录到 MEMORY.md
2. 向子修汇报
3. 等待 Yellow 决策

---

_本规范参考 VLA-Handbook CLAUDE.md 建立_
