# memory/ — WM Research 记忆存储

> 本目录为 OPC-WM 的本地记忆存储，对标 workspace/memory/ 架构。

## 目录结构

```
memory/
├── blog/
│   └── archives/     # VLA-Handbook 社交情报存档
│                     # 每周日从 GitHub API 自动拉取 commit log
├── daily/           # 每日工作日志（YYYY-MM-DD.md）
├── domains/         # 领域详细知识
│   ├── safety-alignment.md    # VLA 安全对齐
│   ├── post-training.md       # 后训练效率
│   └── wm-consistency.md      # WM 长程一致性
└── archive/         # 14天以上旧日志
```

## 使用规则

- 每次心跳前更新 `daily/YYYY-MM-DD.md`
- 每周日汇总到周报后归档到 `archive/`
- 重大发现立即写 `domains/` 相关文件

---
_创建: 2026-04-01 by OPC-WM subagent_
