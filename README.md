# cursor-memory（记忆原型）

本仓库提供两套可在 Cursor **用户层 Rules & Skills** 中注册的**记忆原型**，落盘位于用户各工作区内（参见 [.cursor/rules/project-target.mdc](.cursor/rules/project-target.mdc)）。

## 用户全局 Rules & Skills（本机路径）

将规则与技能放到本机固定目录即可作为**用户全局**配置加载（与具体仓库的 `.cursor/` 无关）：

| 类型 | 路径（类 Unix，`~` 为用户主目录） |
|------|-------------------------------------|
| 规则 | `~/.agents/rules` |
| 技能 | `~/.agents/skills` |

在 **Windows** 上可写为：

- 规则：`%USERPROFILE%\.agents\rules`
- 技能：`%USERPROFILE%\.agents\skills`

可将本仓库中的 `.mdc` 与对应技能目录（如 `stack-memory/.cursor/skills/`、`flow-memory/.cursor/skills/` 下的内容）复制或同步到上述目录；记忆落盘位置由各 `.mdc` 中的**候选 root 路径列表**解析（相对当前工作区）；按需增删或置顶一行路径即可（参见 `project-target.mdc`）。

## 两套体系（共存）

| 体系 | 用途 | 入口（读这里即可上手） |
|------|------|------------------------|
| **stack-memory** | 分层知识库（L0–L3），按需检索规则与模式 | [stack-memory/INDEX.md](stack-memory/INDEX.md)、[stack-memory/README.md](stack-memory/README.md) |
| **flow-memory** | 工作助手分时记忆（目标 / 决策 / 业务上下文 / episodic / summaries） | [flow-memory/README.md](flow-memory/README.md)、规则 [flow-memory/.cursor/rules/flow-memory.mdc](flow-memory/.cursor/rules/flow-memory.mdc)、归档技能 [flow-memory/.cursor/skills/archive-flow-memory/SKILL.md](flow-memory/.cursor/skills/archive-flow-memory/SKILL.md) |

## 默认落盘锚点（分时记忆）

- **根目录**：将 `flow-memory/` 原型目录放到工作区内；读写相对于解析得到的 **root**（须含 `core/`、`episodic/`、`summaries/`），例如 `versions.json` 也在 root 下。
- **配置方式**：打开全局规则中的 [`flow-memory.mdc`](flow-memory/.cursor/rules/flow-memory.mdc)，编辑「候选 root 路径列表」——默认已包含 `./flow-memory/` 与 `./.workspace/flow-memory/` 等；若你的落盘只在 `.workspace` 下，把该行移到列表顶部即可。
- **解析失败**：`use-flow-memory` / `archive-flow-memory` 在无任何候选匹配时会中断并报错，不会向列表外猜测路径。

## 本模板约束（避免隐藏依赖）

- **不包含** persona、world、独立 Memory Recall 技能等外部组件；规则与技能均应在上述路径内自洽。
- 问题清单与工作区笔记（若存在）：`.workspace/problems.md`。
