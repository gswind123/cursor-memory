---
name: archive-flow-memory
description: 当用户明确要求归档工作时（如「归档本轮工作」「记入记忆」「更新工作目标」），将本轮可验证结论写入 flow-memory root 并更新版本表。
---

# flow-memory · 归档流程（archive-flow-memory）

## 契约与引用约定

- **公共契约**：写库触发、目录语义、共用禁止项以规则 **`flow-memory`** 为准；本技能仅在满足该规则中的 **写库触发（Write Trigger）** 时执行。
- **按名字引用**：仅用名称指涉规则或其它技能（如 **`flow-memory`**、**`use-flow-memory`**），不使用仓库内文件路径。

## 启用条件

用户消息须满足规则 **`flow-memory`** 的 **写库触发**（明确归档或更新记忆的意图）。示例（不必逐字）：

- 「归档本轮工作」「把工作记下来」「记入记忆」
- 「更新工作目标」「同步本周目标」
- 「记录决策 / 约束」「更新业务上下文」（写入对应 core 文件）

未表达上述意图时 **不要**执行本技能。

## 执行原则（归档侧）

- **只写可验证结论**：决策、目标、约束、业务要点、协作偏好差分；不写聊天逐字原文。
- **禁止**（与契约一致，此处强调写入形态）：`emotion`、角色扮演式关系叙述、个人生活细节、敏感凭证。
- **Episodic**：当日摘要条目；复杂稳定信息归 **core**。

## 执行步骤

1. **理解范围**：按用户指令判断主要写入目标（目标 / 决策与约束 / 业务上下文 / 协作偏好 / 当日流水 / 摘要）。
2. **更新 Episodic**：写入或追加 `episodic/YYYY/YYYY-MM-DD.md`，记录本轮**做了什么、结论、待跟进**；frontmatter 至少包含 `type`、`date`、`importance`、`recall_triggers`：
   - `type` 固定使用 **`work_log`**。
   - **不要**包含 `emotion`。
3. **更新 Core（按需）**：
   - 目标相关 → `core/work_goals.md`
   - 决策 / 约束 → `core/decisions_and_constraints.md`
   - 业务 / 领域上下文 → `core/project_context.md`
   - 协作方式 / 边界 → `core/collaboration.md`
   - 里程碑节点 → `core/timeline.md`（`YYYY-MM-DD` 条目）
4. **更新 Summaries（按需）**：在 `summaries/long_term.md` 或 `summaries/weekly.md` 补充跨会话仍重要的摘要；可注明日期与 `recall_triggers` 关键词。
5. **版本表**：本次新增或重要修订，生成版本号 **YYYYMMDD-序号**（如 `20300101-1`），追加到 **`versions.json`** 的 `entries`：`version`、`source`（episodic | core | summaries）、`path`（相对 flow-memory **root**）、`createdAt`（ISO8601）。

## Episodic frontmatter 示例

```yaml
---
type: work_log
date: YYYY-MM-DD
importance: medium
recall_triggers: ["模块名", "关键词"]
---
```

可选：`section_briefs`（段落锚点 → 一句话摘要）。

### 外部信息摘要（用户明确要求记住某条外部信息时）

可在段落旁或简短 frontmatter 中注明 `topic`、`date`、`recall_triggers`；保持中性一句话摘要，不含敏感原文。

## 完成后

向用户做**简短确认**，并给出写入要点摘要。

## 输出示例

```
已归档工作记忆 — [一句话摘要，说明更新了哪些文件层级]
```

## 可能创建/更新的文件（相对 flow-memory root）

- `episodic/YYYY/YYYY-MM-DD.md`
- `core/work_goals.md`、`core/decisions_and_constraints.md`、`core/project_context.md`、`core/collaboration.md`、`core/timeline.md`
- `summaries/long_term.md`、`summaries/weekly.md`
- `versions.json`
