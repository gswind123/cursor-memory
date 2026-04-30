# stack-memory · 分层记忆索引

先定位条目再精读；避免递归扫描全库。写入后须保持本文件与相关 `README.md` 同步（见 [README.md](README.md) 写入契约）。

## 快速入口

| 用途 | 路径 |
|------|------|
| 体系说明与写入契约 | [`README.md`](README.md) |
| 硬规则（L0） | [`L0_system_rules/README.md`](L0_system_rules/README.md) |
| L1 总说明 | [`L1_project_knowledge/README.md`](L1_project_knowledge/README.md) |
| **当前工作目标**（可写入） | [`L1_project_knowledge/work_goals.md`](L1_project_knowledge/work_goals.md) |
| **决策与约束**（可写入） | [`L1_project_knowledge/decisions_and_constraints.md`](L1_project_knowledge/decisions_and_constraints.md) |
| **项目业务与上下文**（可写入） | [`L1_project_knowledge/project_context.md`](L1_project_knowledge/project_context.md) |
| 指令参数手册（自管） | `L1_project_knowledge/<your_cookbook>.md` |
| 参数组合模式（自管） | `L1_project_knowledge/<your_combo_patterns>.md` |
| Few-shot 总入口 | [`L2_examples/README.md`](L2_examples/README.md) |
| **工作助手示例分类** | [`L2_examples/work_assistant/README.md`](L2_examples/work_assistant/README.md) |
| 避错总入口 | [`L3_feedback/README.md`](L3_feedback/README.md) |
| **工作助手避错分类** | [`L3_feedback/work_assistant/README.md`](L3_feedback/work_assistant/README.md) |

## L0 · 硬规则

- `L0_system_rules/<rule>.md`：格式/契约、不可违背约束。**归档技能默认不写入 L0。**

## L1 · 项目知识（可写入主落点）

- 目标、决策/约束、业务上下文见上表；其余 `*.md` 为方法论/手册/模式（由你维护）。

## L2 · 极简示例

- `L2_examples/<category>/README.md`：分类说明
- `L2_examples/<category>/<pattern>.md`：1～3 行/段级片段

## L3 · 踩坑与反例

- `L3_feedback/<category>/README.md`：分类说明
- `L3_feedback/<category>/<pitfall>.md`：现象 → 原因 → 修正

## 权力顺序

**L0 > L1 > L2 > L3**（L2/L3 不得推翻 L0/L1）。
