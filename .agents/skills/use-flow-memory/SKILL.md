---
name: use-flow-memory
description: 仅当用户显式提及 memory、记忆、偏好、风格、历史项目或与记忆相关的长期上下文，并要求参考 flow-memory（分时记忆）时启用：只读检索并按约束输出；不写入、不归档、不调用 archive-flow-memory。（泛化请求未点名记忆则不触发）
---

# flow-memory · 只读流程（use-flow-memory）

## 契约与引用约定

- **目录语义与禁止项**：见与本技能同目录的 **`reference.md`**（**不含** root 解析）。
- **Root 解析（候选路径、合法性检查、算法）**：**唯一**以技能 **`search-memory-storage`** 为准；本技能只约定 **memoryType = `flow-memory`** 时的读取顺序与输出。
- **按名字引用**：提及其它技能时仅用名称（如 **`archive-flow-memory`**、**`search-memory-storage`**），不使用仓库内文件路径。

## 启用条件

当用户**明确希望本次回答参考 flow-memory 落盘内容**且意图为**只读参考**（非归档）时启用本技能。典型情形：

- 用户在 Cursor 中**附加了本技能**，并要求据此检索记忆；或
- 用户消息中同时包含「memory / 记忆 / 偏好 / 风格 / 历史项目 / 以往习惯」一类用语，且明确指向 **flow-memory**、**分时记忆**，或 core / episodic / summaries 式检索。

**弱触发（不要启用）**：仅「帮我写 API」「重构这段代码」等，未附加本技能且未要求参考 flow-memory。

## 不适用

- 用户意图为**写入 / 归档**：改用技能 **`archive-flow-memory`**；本技能不修改任何落盘文件。

## 只读边界（硬约束）

- **禁止**创建、修改、删除 flow-memory **root** 下任意文件（含 `versions.json`、`recall_state.json`）。
- **禁止**执行技能 **`archive-flow-memory`** 或 **`archive-stack-memory`** 的写入流程。
- 仅读取与当前任务相关的必要片段，完成当前回答。

## Root 解析（必须先执行）

1. **加载并严格执行**技能 **`search-memory-storage`** 的全文算法，指定 **memoryType = `flow-memory`**。
2. **第一步**：按 **`search-memory-storage`** 中的候选基准目录列表与拼接规则，自上而下得到候选 root；第一个通过 **`search-memory-storage`** 所列 **flow-memory** 合法性检查的目录即为本次任务的 **root**。
3. **禁止**在 **`search-memory-storage`** 所列候选之外猜测路径；**禁止**自动创建目录或「假定」root。

### Root 解析失败（静默软降级）

若无有效 root（依 **`search-memory-storage`** 判定无效）：

1. **不读取**任何记忆文件；不向候选列表外猜测路径。
2. **不输出**错误提示，也不输出「未加载 memory」类说明（**静默**）。
3. **继续完成用户主任务**：按行业默认最佳实践作答；**跳过**下文「读取顺序」。
4. **禁止**在输出中假装已读过记忆、编造记忆条目或引用不存在的落盘内容。

## 读取顺序（少而精）

**仅当 root 已成功解析时执行。** 相对 flow-memory **root**，按优先级读取与任务最相关的少量文件（不必全盘打开）：

1. `core/work_goals.md`
2. `core/decisions_and_constraints.md`
3. `core/project_context.md`
4. `core/collaboration.md`
5. `core/timeline.md`
6. 近期 `episodic/YYYY/YYYY-MM-DD.md`（当日或近日）
7. `summaries/long_term.md`、`summaries/weekly.md`

## 输出契约

1. **Memory 约束提要**：**仅当 root 已成功解析时**输出；列出与任务直接相关的要点（建议 3–7 条）；注明类别（如目标 / 决策与约束 / 业务上下文 / 协作 / 时间线 / 流水摘要）。若 root 未解析（静默软降级），**整节省略**。
2. **回答正文**：若 root 已解析，按上述记忆约束实现；逐条对齐；若某条在 memory 中**未找到**，标注「memory 未提供」并以行业默认最佳实践补全且声明为推断。若 root **未**解析，直接按默认最佳实践完成主任务，**不得**假装已读记忆。
3. **仅当 root 已成功解析时**：若某文件缺失或某条目为空，说明情况并按第 2 条标注「memory 未提供」与推断。

## 用户可复制的强触发话术（示例）

以下话术有助于**显式触发**只读检索（可与附加本技能配合使用）：

**方法 1 · 显式唤醒**

> 在回答前请先读 **flow-memory**，并把其中与本次任务相关的偏好与约束当作主约束。

**方法 2 · 点名内容类型**

> 基于我以往技术栈与编码偏好（memory），请先读 **flow-memory** 再完成：……

**方法 3 · 先加载再执行**

> 先总结你从 **flow-memory** 得到的与本次相关的约束提要，再基于该提要完成任务。
