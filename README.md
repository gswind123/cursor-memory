# cursor-memory（记忆原型）

本仓库提供两套**记忆落盘模板**（`flow-memory/`、`stack-memory/`），以及一组安装在 Cursor **用户全局 Skills** 下的技能（见仓库内 [`.agents/skills/`](.agents/skills/)）。工作区目标说明见 [.cursor/rules/project-target.mdc](.cursor/rules/project-target.mdc)。

## User Rules vs Skills（重要）

- Cursor **Preferences / User Rules** 中的规则更接近一段**总是注入的提词**，不适合当作可被其它文档「引用」的公共契约库。
- 本仓库将**可执行的契约**放在 **Skills** 内：`SKILL.md` + 同目录 **`reference.md`**；**落盘 root 的查找顺序**由技能 **`search-memory-storage`** 唯一维护。

## 用户全局 Skills（本机路径）

将技能目录复制到本机固定路径即可作为**用户全局**配置加载（与具体仓库的 `.cursor/` 无关）：

| 类型 | 路径（类 Unix，`~` 为用户主目录） |
|------|-------------------------------------|
| 技能 | `~/.agents/skills` |

在 **Windows** 上：`%USERPROFILE%\.agents\skills`

**建议**：把本仓库 [`.agents/skills/`](.agents/skills/) 下下列目录一并同步到上述路径（至少包含 root 解析技能）：

- **`search-memory-storage`** — 配置候选基准目录列表（置顶常用路径）
- **`use-flow-memory`**、**`archive-flow-memory`**
- **`use-stack-memory`**、**`archive-stack-memory`**

记忆**落盘**仍放在各工作区内（如 `./flow-memory/` 或 `./.workspace/flow-memory/`）；是否命中由 **`search-memory-storage`** 解析。

## Cursor 索引与 `.gitignore`（常见坑）

Cursor 在构建索引/检索上下文时，通常会**默认忽略被 `.gitignore` 排除的路径**。如果你把记忆落盘放在被忽略的目录（例如把 `/.workspace/` 加进了 `.gitignore`，而记忆实际在 `./.workspace/flow-memory/` / `./.workspace/stack-memory/`），就可能出现「技能能解析到 root，但 Cursor 检索不到文件内容」的现象。

**解决技巧（最小侵入）**：在工作区放置 `.cursorignore`，用 `!` 把记忆目录**加回**可见范围（规则顺序通常从上到下生效，必要时同时放行父目录）。

示例（按你的实际目录调整）：

```txt
# 仍然忽略整个 .workspace（若你需要）
.workspace/**

# 但把记忆落盘加回索引/检索范围
!.workspace/flow-memory/**
!.workspace/stack-memory/**
```

## 两套体系（共存）

| 体系 | 用途 | 落盘模板入口 |
|------|------|----------------|
| **stack-memory** | 分层知识库（L0–L3），按需检索规范与模式 | [stack-memory/INDEX.md](stack-memory/INDEX.md)、[stack-memory/README.md](stack-memory/README.md) |
| **flow-memory** | 分时记忆（目标 / 决策 / 业务上下文 / episodic / summaries） | [flow-memory/README.md](flow-memory/README.md) |

触发读写流程：在对话中显式要求参考 **flow-memory** / **stack-memory**，或使用 **`use-*`** / **`archive-*`** 技能（详见各 `SKILL.md`）。

## 默认落盘与 root 配置

- **分时 flow-memory**：root 下须含目录 **`core/`**、`episodic/`、`summaries/`（另见模板目录说明）。
- **分层 stack-memory**：root 下须含 **`INDEX.md`** 与 **`L1_project_knowledge/`**。
- **配置查找顺序**：编辑已安装技能 **`search-memory-storage`** 内的「候选基准目录列表」。
- **解析失败**：**`use-*`** 静默当作无记忆继续主任务；**`archive-*`** 硬中断并报错（修复入口仍为 **`search-memory-storage`**）。

## 本模板约束（避免隐藏依赖）

- **不包含** persona、world、独立 Memory Recall 技能等外部组件；契约应在 `.agents/skills` 内自洽。
- 本仓库**不提供**可安装的独立 `.mdc` 记忆规则文件；契约以 Skills 为准。
- 问题清单与工作区笔记（若存在）：`.workspace/problems.md`。
