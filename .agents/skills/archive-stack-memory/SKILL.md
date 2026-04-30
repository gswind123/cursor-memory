---
name: archive-stack-memory
description: 用户明确要求归档到 stack-memory 时，将可泛化的结论写入 L1/L2/L3，并同步 INDEX 与相关 README（不显式触发则不执行）。
---

# stack-memory · 归档流程（archive-stack-memory）

## 契约与引用约定

- **分层语义、权力顺序与禁止项**：见与本技能同目录的 **`reference.md`**（**不含** root 解析）。
- **Root 解析（候选路径、合法性检查、算法）**：**唯一**以技能 **`search-memory-storage`** 为准；本技能定义 **memoryType = `stack-memory`** 时的写入步骤。
- **按名字引用**：仅用名称指涉其它技能（如 **`use-stack-memory`**、**`search-memory-storage`**），不使用仓库内文件路径。

## 启用条件

用户消息须表达**明确的归档或写入 stack-memory 的意图**。示例（不必逐字）：

- 「归档到 stack-memory」「写入分层记忆」
- 「记入 L1」「更新工作目标 / 决策 / 项目上下文」
- 「加一个 L2 示例」「把这个坑记到 L3」

未表达归档意图时 **不要**执行本技能。

## 写入与权力顺序

遵守 **`reference.md`** 中的 **L0 > L1 > L2 > L3**。写入内容不得与 L0/L1 冲突；若冲突须在 L3 标注「待与 L1 对齐」而非覆盖硬规则。

## 默认写入映射

| 用户意图（摘要） | 优先文件 |
|------------------|----------|
| 当前目标、里程碑对齐 | `L1_project_knowledge/work_goals.md` |
| 决策、约束、不可违背项 | `L1_project_knowledge/decisions_and_constraints.md` |
| 业务、术语、流程 | `L1_project_knowledge/project_context.md` |
| 可泛化的极简写法 | `L2_examples/<category>/<pattern>.md`（缺省可用 `work_assistant/`） |
| 踩坑、反例、修正 | `L3_feedback/<category>/<pitfall>.md`（缺省可用 `work_assistant/`） |

## 禁止（归档侧）

- **不写 L0**（除非用户明确要求新增硬规则且给出可引用证据/契约；不确定时写入 L1「待升格」而非 L0）。
- 不写入：敏感信息、个人生活、聊天逐字长文、不可泛化的一次性细节。
- 不调用 **`reference.md`** 未声明、未与用户约定的其它规则或技能。

## Root 解析（必须先执行）

1. **加载并严格执行**技能 **`search-memory-storage`** 的全文算法，指定 **memoryType = `stack-memory`**。
2. **第一步**：按 **`search-memory-storage`** 中的候选基准目录列表与拼接规则，自上而下得到候选 root；第一个通过 **stack-memory** 合法性检查的目录即为 **root**。
3. **禁止**在 **`search-memory-storage`** 所列候选之外猜测路径；**禁止**自动创建 root；**禁止**在解析失败时创建任何文件。

### Root 解析失败（硬中断）

若无有效 root：

1. **停止**：不执行下文「执行步骤」；不创建、不修改任何文件。
2. 仅向用户输出**错误说明**，须包含：**诊断**（未解析到有效 stack-memory root）、**修复**（将 stack-memory 原型放到可由 **`search-memory-storage`** 解析到的路径，或**打开并编辑**技能 **`search-memory-storage`** 内的「候选基准目录列表」）。
3. **禁止**在报错中粘贴多套具体路径列表；**禁止**向列表外搜索。

## 执行步骤

**仅当 root 已成功解析后**执行下列步骤。

1. **归类**：判断材料属于目标 / 决策约束 / 上下文 / 示例 / 踩坑中的哪些。
2. **更新 L1**：按需追加或修订 `work_goals.md`、`decisions_and_constraints.md`、`project_context.md`；条目短小、可验证。
3. **可选 L2**：仅当能提炼为 1～3 行/段级模式时，写入 `L2_examples/<category>/<new_or_existing>.md`。
4. **可选 L3**：现象→原因→修正，写入 `L3_feedback/<category>/<new_or_existing>.md`。
5. **索引同步**：若新建了 **`L2_examples/` 或 `L3_feedback/` 下的新分类目录**或新的顶层条目文件名，必须更新：
   - root **`INDEX.md`**「快速入口」或分层列表中的链接；
   - 对应层的 **`README.md`** 或分类内 **`README.md`** 中的条目列表。
6. **确认**：向用户简短说明写入了哪些路径、是否更新了索引。

## 完成后输出示例

```
已写入 stack-memory — L1: …；L2/L3: …；已更新 INDEX: 是/否
```

## 常触及文件（相对 stack-memory root）

- `L1_project_knowledge/work_goals.md`
- `L1_project_knowledge/decisions_and_constraints.md`
- `L1_project_knowledge/project_context.md`
- `L2_examples/work_assistant/*.md`（示例）
- `L3_feedback/work_assistant/*.md`（示例）
- `INDEX.md`（新建分类/顶层条目时必更）

## L1 维护建议（可选）

- 「组合模式」类文件可在顶部维护 **`## 模式目录`** 作为单一事实来源。
- `work_goals.md` 宜定期滚动：当前焦点 + 少量历史一行摘要，避免 L1 膨胀。
