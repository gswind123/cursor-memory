# flow-memory（工作助手 · 分时记忆）

本目录约定 **flow-memory** 分时记忆落盘的**目录结构**与各文件的**内容语义**；仅描述「写什么、放在哪」，不包含工具配置或操作说明。

## 目录与文件角色

### Core（中期、谨慎改）

| 文件 | 内容 |
|------|------|
| `core/work_goals.md` | 当前阶段工作目标（本周 / 本迭代） |
| `core/decisions_and_constraints.md` | 关键决策、约束与不可违背项（宜写清原因） |
| `core/project_context.md` | 项目业务特性、领域术语、关键流程（相对稳定） |
| `core/collaboration.md` | 协作偏好与边界（输出风格、沟通节奏、禁忌） |
| `core/timeline.md` | 项目里程碑与按日节点摘要 |

### Episodic（短期）

| 路径 | 内容 |
|------|------|
| `episodic/YYYY/YYYY-MM-DD.md` | 当日工作流水与可验证结论（短条目，非逐字对话） |

### Summaries（长期）

| 文件 | 内容 |
|------|------|
| `summaries/long_term.md`、`summaries/weekly.md` | 从 core / episodic 提炼的跨阶段或跨周摘要 |

### Episodic 建议 frontmatter（写入条目时可选）

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

## 写入与版本记录

内容变更写入上述对应路径。重要修订可在本目录根下的 **`versions.json`** 中追加条目：`path` 为相对于本目录（flow-memory）根的路径。

## 目录完整性（约定）

作为有效的 flow-memory 落盘根目录，应同时包含下列子目录：

- `core/`
- `episodic/`
- `summaries/`

示例根目录名可为 `flow-memory/`；若置于其它路径，仍须保持上述结构。
