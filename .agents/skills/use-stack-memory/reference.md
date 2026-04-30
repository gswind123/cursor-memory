# stack-memory · 目录契约（参考）

> 不含 root 路径解析；落盘位置仅由技能 **`search-memory-storage`** 定义。

## 定位

- **stack-memory**：分层记忆原型（RAG 式知识库）；不作长篇正文仓库；不引入 persona/world 等契约外依赖。
- 本节只定义分层语义与共用边界；**何时只读检索**由 **`use-stack-memory`** 定义。

## 分层 schema 与权力顺序

- **L0_system_rules/**：硬规则（格式/契约/不可违背）。
- **L1_project_knowledge/**：方法论、参数语义、组合模式；工作助手主写入文件包括 `work_goals.md`、`decisions_and_constraints.md`、`project_context.md`。
- **L2_examples/**：极简示例（约 1～3 行/段）；**不得**推翻 L0/L1。
- **L3_feedback/**：踩坑与反例（现象→原因→修正）；不作风格来源，**不得**推翻 L0/L1。

权力顺序：**L0 > L1 > L2 > L3**。

**检索习惯（契约层）**：先读 root **`INDEX.md`** 再跟链接条目；单次任务少引用，避免递归扫全库。

## 共用禁止项（读）

- 不依赖本节未声明的其它规则或外部流程。
