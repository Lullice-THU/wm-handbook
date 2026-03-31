# WM-Research 自主维护计划

_本文件定义 OPC-WM 如何自主维护 GitHub 仓库，减少对子修的依赖。_

---

## Git 快速参考

```bash
# 标准提交流程（每次完成工作后执行）
git add -A
git commit -m "描述本次更新内容"
git push origin main

# 查看状态
git status

# 查看远程
git remote -v
```

---

## 提交规范

### 何时 commit
- 每次完成任何有意义的工作后**立即 commit**，不堆积
- 不等周、不等月底
- 一个 commit 对应一个逻辑变更（如：新增1篇论文解析、更新1家公司档案、修复1个错误）

### Commit 消息格式
```
<类型>: <简短描述>

可选的详细说明（超过50字时写这里）
```

**类型前缀：**
| 前缀 | 适用场景 |
|------|---------|
| `feat:` | 新增文件、新内容、新功能 |
| `update:` | 更新已有内容（论文、行业动态） |
| `fix:` | 修正错误、补充遗漏 |
| `doc:` | 文档修改（README、CHANGELOG、内存文件） |
| `refactor:` | 重构、整理结构 |
| `weekly:` | 周报生成 |

**示例：**
```bash
git commit -m "feat: 新增 ATOMVLA 理论解析"
git commit -m "update: 补充 1X Neo Beta 最新进展"
git commit -m "weekly: 第2期周报 2026-04-07"
git commit -m "fix: 修正 PAPERS.md 中 3 篇论文链接"
```

---

## 目录清理与 .gitignore

### 需排除的文件/目录

以下文件不应进入 Git 仓库：

```
# OpenClaw 工作状态文件
.openclaw/
.openclaw/workspace-state.json

# OS 临时文件
.DS_Store
.AppleDouble
._*

# Python 缓存
__pycache__/
*.pyc
*.pyo

# IDE 配置（按需）
.vscode/
.idea/
*.swp
*.swo
```

### .gitignore 内容

已在仓库根目录创建 `.gitignore`，内容如下：

```
# OpenClaw
.openclaw/

# macOS
.DS_Store
._*

# Python
__pycache__/
*.pyc

# Editor
.vscode/
.idea/
*.swp
```

---

## 协同方式

### opc-wm 自主 push（默认）
- opc-wm 自主决定何时 commit + push
- 子修只在**有重大问题**时介入
- 不需要每次 push 都通知子修

### 子修介入条件
- Git 冲突无法自行解决
- 需要变更仓库名称或结构
- Yellow 提出特殊需求
- GitHub Token 过期/失效

### 重大更新通知
- 首次成功 push → 通知子修
- 重大里程碑（如 Phase 2 启动）→ 通知子修
- 报错/异常 → 通知子修

---

## 长期维护节奏

### 每周日 — 例行维护
1. 完成本周工作（论文、理论、周报）
2. `git add -A && git commit -m "weekly: YYYY-WXX 周报"`
3. `git push origin main`
4. 如果当天没有任何改动，**不需要 push**

### 有重大发现时 — 随时 push
- 重要论文解析完成
- 行业重大进展
- Phase 里程碑完成

### 月度整理
- 检查 `.gitignore` 是否覆盖了新产生的临时文件
- 检查 docs/ 目录结构是否需要调整
- 清理过期的 CHANGELOG 条目

---

## Git 操作安全注意事项

⚠️ **不要执行的危险操作：**
```bash
# ❌ 禁止强制 push（会覆盖远程历史）
git push -f origin main

# ❌ 禁止删除远程分支
git push origin --delete <branch>

# ❌ 禁止修改 .git/config 以外的 remote 配置
```

✅ **安全操作：**
```bash
# ✅ 始终先查看状态再 push
git status

# ✅ 始终使用 standard commit + push 流程
git add -A
git commit -m "..."
git push origin main

# ✅ 如有冲突，先 pull 再解决
git pull origin main
# 解决冲突后
git add -A
git commit -m "fix: resolve merge conflict"
git push origin main
```

---

## 故障处理

| 问题 | 解决方法 |
|------|---------|
| `Permission denied` | Token 可能过期，检查 git remote 或重新配置 |
| `src refspec main does not match` | 分支名错误，检查当前分支 |
| 冲突无法解决 | 联系子修协助 |
| `.gitignore` 不生效 | `git rm -r --cached .` 然后重新 add |

---

_本计划由 OPC-WM 于 2026-04-01 制定_
