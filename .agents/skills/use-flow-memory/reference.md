# flow-memory · 目录契约（参考）

> 不含 root 路径解析；落盘位置仅由技能 **`search-memory-storage`** 定义。

## 定位

- **flow-memory**：分时记忆原型（短期流水 / 中期核心 / 长期摘要）。
- 本节只定义目录语义与共用边界；**何时只读检索**由 **`use-flow-memory`** 定义。

## 目录 schema（语义）

1. **Episodic** — `episodic/YYYY/YYYY-MM-DD.md`：短期工作流水（摘要级结论，非逐字对话）。
2. **Core** — 中期核心（修改需谨慎）：
   - `core/work_goals.md` — 当前阶段工作目标。
   - `core/decisions_and_constraints.md` — 决策与约束。
   - `core/project_context.md` — 业务与领域上下文。
   - `core/collaboration.md` — 协作偏好与边界。
   - `core/timeline.md` — 里程碑与时间线节点。
3. **Summaries** — `summaries/long_term.md`、`summaries/weekly.md`：长期滚动摘要。

根目录可选 **`recall_state.json`**：预留占位，默认不绑定独立召回流程。

## 共用禁止项（读）

- 不使用 `emotion` 或虚拟人式「关系叙事」字段。
- 不依赖本节未声明的其它规则或外部流程（无隐藏依赖）。
