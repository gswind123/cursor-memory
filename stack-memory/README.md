# stack-memory（分层记忆原型）

本目录约定 **stack-memory** 分层记忆落盘的**目录结构**、**各层语义**与**维护契约**；仅描述「写什么、放在哪、索引如何保持」，不包含工具配置或操作说明。

## 与 flow-memory 的分工（内容形态）

| 体系 | 更擅长沉淀的内容 |
|------|------------------|
| **flow-memory** | 按时间的流水（episodic）、稳定 core（目标/决策等）、周/长期摘要 |
| **stack-memory**（本目录） | 可复用的规范、模式、极简示例与避错（分层组织 + 结构化写入） |

若同一工作区同时存在两套落盘，可按「偏时间线」与「偏分层模式」自行选择写入目标；本目录不规定外部选择方式。

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

## 写入契约

### 什么写入哪一层

| 类型 | 落点 |
|------|------|
| 当前阶段工作目标（允许频繁变） | `L1_project_knowledge/work_goals.md` |
| 决策与约束（含原因） | `L1_project_knowledge/decisions_and_constraints.md` |
| 业务、术语、关键流程 | `L1_project_knowledge/project_context.md` |
| 可泛化的极简写法（1～3 行/段） | `L2_examples/<category>/<pattern>.md` |
| 可复现的坑（现象→原因→修正） | `L3_feedback/<category>/<pitfall>.md` |
| 格式/解析级硬规则 | **默认不向 L0 写入**；仅在有权威证据且明确需要时新增 `L0_system_rules/*.md` |

### 禁止写入

- 敏感凭证、令牌、隐私与个人生活细节。
- 聊天逐字原文；只沉淀**结论与可复查要点**。
- 无法脱离具体情境泛化的闲话。

### `work_goals.md` 滚动建议

保留「当前焦点」+ 可选「最近 1～2 阶段一行摘要」，避免 L1 无限膨胀。

### 索引义务

新建 **`L2_examples/`、`L3_feedback/` 下的分类目录**，或新增需在索引中暴露的顶层条目时，必须同步：

1. 根目录 **`INDEX.md`**
2. 对应层或分类下的 **`README.md`**

## 在库内定位条目（约定）

1. 从 [`INDEX.md`](INDEX.md) 定位。
2. 权力顺序：**L0 > L1 > L2 > L3**（示例与避错不得推翻硬规则与 L1 方法论）。
3. **少而精**：每次只展开与当前问题最相关的少量段落。

## 维护入门

1. 保持根目录存在 **`INDEX.md`** 与 **`L1_project_knowledge/`**（以及按需展开的 L0/L2/L3）。
2. 新增或调整条目后，按上文「索引义务」更新 `INDEX.md` 与相关 `README.md`。
3. 示例根目录名可为 `stack-memory/`；置于其它路径时，仍须保持本 README 所述层级结构。

## 子模块（可选）

若需被主工程引用，可用 Git Submodule；版本管理仍在记忆仓库内完成。
