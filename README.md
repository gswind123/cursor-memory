# cursor-memory（记忆原型）

本仓库提供两套可在 Cursor **用户层 Rules & Skills** 中注册的**记忆原型**，落盘位于用户各工作区内（参见 [.cursor/rules/project-target.mdc](.cursor/rules/project-target.mdc)）。

## 两套体系（共存）

| 体系 | 用途 | 入口（读这里即可上手） |
|------|------|------------------------|
| **stack-memory** | 分层知识库（L0–L3），按需检索规则与模式 | [stack-memory/INDEX.md](stack-memory/INDEX.md)、[stack-memory/README.md](stack-memory/README.md) |
| **flow-memory** | 工作助手分时记忆（目标 / 决策 / 业务上下文 / episodic / summaries） | [flow-memory/README.md](flow-memory/README.md)、规则 [flow-memory/.cursor/rules/flow-memory.mdc](flow-memory/.cursor/rules/flow-memory.mdc)、归档技能 [flow-memory/.cursor/skills/archive-flow-memory/SKILL.md](flow-memory/.cursor/skills/archive-flow-memory/SKILL.md) |

## 默认落盘锚点（分时记忆）

- **根目录**：将 `flow-memory/` 整个目录置于你的工作区后，记忆文件相对于该目录读写（如 `episodic/`、`core/`、`summaries/`、`versions.json`）。
- 若你希望落在 `.workspace/` 下，可复制该目录到 `./.workspace/flow-memory/` 并在用户规则中把「落盘根路径」指向该位置（见 `project-target.mdc` 中的映射约定）。

## 本模板约束（避免隐藏依赖）

- **不包含** persona、world、独立 Memory Recall 技能等外部组件；规则与技能均应在上述路径内自洽。
- 问题清单与工作区笔记（若存在）：`.workspace/problems.md`。
