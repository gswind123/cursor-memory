# stack-memory（分层记忆原型）

本目录是 Cursor **用户级**可注册的 **stack-memory 记忆原型** 落盘：把知识按 **L0–L3** 分层，支持 **检索（拉起）** 与 **显式归档（写入）** 两种记忆迭代方式。  
规则见 [`.cursor/rules/stack-memory.mdc`](.cursor/rules/stack-memory.mdc)；归档见 [`.cursor/skills/archive-stack-memory/SKILL.md`](.cursor/skills/archive-stack-memory/SKILL.md)。

## 与 flow-memory 的分工

| 体系 | 更擅长 |
|------|--------|
| **flow-memory** | 按时间的流水（episodic）、稳定 core（目标/决策等）、周/长期摘要 |
| **stack-memory**（本目录） | **可复用**的规范、模式、极简示例与避错（RAG 式分层检索 + 结构化写入） |

同一工作区可同时存在两套落盘根；写入前根据「偏时间线」还是「偏分层模式」选择体系。

## 推荐目录结构（最小）

```text
stack-memory/
├── README.md                 # 本文件
├── INDEX.md                  # 总索引（先索引后条目）
├── L0_system_rules/
├── L1_project_knowledge/
│   ├── work_goals.md              # 当前目标（可变）
│   ├── decisions_and_constraints.md
│   └── project_context.md
├── L2_examples/
│   └── <category>/
└── L3_feedback/
    └── <category>/
```

## 写入契约（记忆迭代）

### 什么写入哪一层

| 类型 | 落点 |
|------|------|
| 当前阶段工作目标（允许频繁变） | `L1_project_knowledge/work_goals.md` |
| 决策与约束（含原因） | `L1_project_knowledge/decisions_and_constraints.md` |
| 业务、术语、关键流程 | `L1_project_knowledge/project_context.md` |
| 可泛化的极简写法（1～3 行/段） | `L2_examples/<category>/<pattern>.md` |
| 可复现的坑（现象→原因→修正） | `L3_feedback/<category>/<pitfall>.md` |
| 格式/解析级硬规则 | **默认不归档写入**；仅在有权威证据且用户明确要求时新增 `L0_system_rules/*.md` |

### 禁止写入

- 敏感凭证、令牌、隐私与个人生活细节。
- 聊天逐字原文；只沉淀**结论与可复查要点**。
- 无法脱离单次会话泛化的闲话。

### `work_goals.md` 滚动建议

保留「当前焦点」+ 可选「最近 1～2 阶段一行摘要」，避免 L1 无限膨胀。

### 索引义务

新建 **`L2_examples/`、`L3_feedback/` 下的分类目录**，或新增需在索引中暴露的顶层条目时，必须同步：

1. 根目录 **`INDEX.md`**
2. 对应层或分类下的 **`README.md`**

## 检索（拉起）

1. 从 [`INDEX.md`](INDEX.md) 定位。
2. 权力顺序：**L0 > L1 > L2 > L3**（示例与避错不得推翻硬规则与 L1 方法论）。
3. **少而精**：单次任务只读少量最相关段落。

## 归档（写入）

使用 **显式指令** 触发（示例）：「归档到 stack-memory」「更新 L1 决策」「把这个坑写到 L3」。  
具体步骤见 [`archive-stack-memory` 技能](.cursor/skills/archive-stack-memory/SKILL.md)。

## 快速开始

1. 将 `stack-memory/` 置于工作区（或 `.workspace/stack-memory/`）；在全局 `stack-memory.mdc` 中按需编辑「候选 root 路径列表」，把你的路径置顶即可。
2. 在 Cursor **User Rules & Skills** 中注册 `stack-memory.mdc` 与 `archive-stack-memory`。
3. 从 [`INDEX.md`](INDEX.md) 开始维护条目。

## 子模块（可选）

若需被主工程引用，可用 Git Submodule；版本管理仍在记忆仓库内完成。
