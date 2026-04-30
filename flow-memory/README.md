# flow-memory（工作助手 · 分时记忆）

面向 **Cursor 工作助手** 的分时记忆模板：落盘在工作区内，规则与技能复制到用户层 **Rules & Skills** 后生效。根路径约定见 [.cursor/rules/flow-memory.mdc](.cursor/rules/flow-memory.mdc)。

## 记忆模型（字段与分层职责）

### 检索优先级（由高到低）

1. **`core/work_goals.md`** — 当前阶段工作目标（本周 / 本迭代）。
2. **`core/decisions_and_constraints.md`** — 关键决策、约束与不可违背项（宜写清原因）。
3. **`core/project_context.md`** — 项目业务特性、领域术语、关键流程（相对稳定）。
4. **`core/collaboration.md`** — 协作偏好与边界（输出风格、沟通节奏、禁忌）。
5. **`core/timeline.md`** — 项目里程碑与按日节点摘要。
6. **`episodic/YYYY/YYYY-MM-DD.md`** — 当日工作流水与可验证结论（短条目，非逐字对话）。
7. **`summaries/long_term.md`**、`summaries/weekly.md` — 跨周 / 跨阶段的滚动摘要。

### 各层写什么

| 层级 | 路径 | 写什么 |
|------|------|--------|
| Core（中期、谨慎改） | `core/*.md` | 目标、决策与约束、业务上下文、协作偏好、时间线节点 |
| Episodic（短期） | `episodic/YYYY/YYYY-MM-DD.md` | 当日做了什么、结论、待跟进（摘要级） |
| Summaries（长期） | `summaries/*.md` | 从 core/episodic 提炼的跨会话摘要 |

### Episodic 建议 frontmatter（归档时使用）

```yaml
---
type: work_log
date: YYYY-MM-DD
importance: low | medium | high
recall_triggers: ["关键词", "模块名"]
---
```

可选：`section_briefs`（段落锚点 → 一句话）。**不要**使用 `emotion` 或与角色扮演相关的字段。

### 明确禁止写入的内容

- 情绪 / 情感标签（如 `emotion`）及虚拟人式「关系叙事」。
- 与工作无关的个人生活细节。
- 敏感信息（账号密码、令牌、身份证号等）。
- 聊天逐字原文；只沉淀**可验证的结论与摘要**。

## 写入（归档）

用户使用 **显式指令** 触发（示例：「归档本轮工作」「记入记忆」「更新工作目标」）。执行步骤见技能：

[`archive-flow-memory`](.cursor/skills/archive-flow-memory/SKILL.md)

版本记录写入根目录 **`versions.json`**（`path` 相对于解析得到的 **root**）。

## 与工作区锚点

落盘位置由规则 [`flow-memory.mdc`](.cursor/rules/flow-memory.mdc) 中的 **候选 root 路径列表**解析：默认已包含 `./flow-memory/`、`./.workspace/flow-memory/` 等。若你的目录只在 `.workspace` 下，把对应路径**置顶**或加入自定义行即可；目录结构（`core/`、`episodic/`、`summaries/`）保持不变。无任何候选匹配时，读写技能会**中断并报错**。
