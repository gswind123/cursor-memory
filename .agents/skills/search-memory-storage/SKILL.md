---
name: search-memory-storage
description: 解析当前工作区内 flow-memory / stack-memory 的落盘 root：仅通过锚点文件名在工作区内定位；供 use-flow-memory、archive-flow-memory、use-stack-memory、archive-stack-memory 在读写前执行。无需配置路径列表。
---

# search-memory-storage · 记忆落盘 root 解析

## 定位

- **唯一约定**：root 必须按下方「解析算法」得出；**禁止**跳过解析、**禁止**按本技能未写明的规则推断路径、**禁止**自动创建 root。
- **读写时机**由调用方技能定义；本技能只产出合法 **root** 或 **无效 root**。
- **不做**目录结构校验：锚点文件的**父目录**即认定为对应体系的 root（完全信任锚点）。

## 强制前置（调用方）

执行 **`use-flow-memory`**、**`archive-flow-memory`**、**`use-stack-memory`**、**`archive-stack-memory`** 前**必须先**完成本节解析。

## memoryType 与锚点文件

| memoryType     | 锚点文件名（精确）   | 文件内标识（备选检索） |
|----------------|----------------------|-------------------------|
| `flow-memory`  | `.flow-memory-root`  | `FLOW_MEMORY_ROOT`      |
| `stack-memory` | `.stack-memory-root` | `STACK_MEMORY_ROOT`     |

锚点为**普通文件**；放置在该记忆体系落盘**根目录**下（与 `core/`、`INDEX.md` 等同级，依体系而定）。

## 解析算法

对给定 **memoryType**：

1. **在工作区内查找**名为上表「锚点文件名」的文件。
   - **必须包含隐藏/点文件**：若所用搜索工具默认忽略点文件，须显式开启「包含隐藏文件」或使用文件树枚举。
2. **备选**：若按文件名搜索不可靠，可用内容检索查找恰好一行 **`FLOW_MEMORY_ROOT`** 或 **`STACK_MEMORY_ROOT`**（与 memoryType 对应），命中文件的**父目录**参与计数（与步骤 1 结果合并去重）。
3. 统计**不同父目录**的数量（同一锚点路径只计一次）：
   - **恰好 1 个** → **root** = 该父目录，结束。
   - **0 个** → **无效 root**。
   - **大于 1 个** → **无效 root**（歧义：须删除或移走多余锚点，仅保留一处）。

**禁止**：候选路径列表、目录名遍历猜测 root、或在本技能外自定锚点名。

## 无效 root · 调用方行为

| 调用方 | 行为 |
|--------|------|
| **`use-flow-memory`** / **`use-stack-memory`** | **静默**：不读落盘；继续主任务；不得假装读过记忆。 |
| **`archive-flow-memory`** / **`archive-stack-memory`** | **硬中断**：不写任何文件；说明无效 root 及消歧方式。 |

**用户修复（摘要）**（不要求改 Preferences、不要求编辑本技能内的路径列表）

1. 在实际使用的记忆**根目录**放入对应锚点文件（可从本仓库原型 `flow-memory/`、`stack-memory/` 复制）。
2. 搜索时**包含隐藏文件**，确保能发现 `.flow-memory-root` / `.stack-memory-root`。
3. **多锚点歧义**：合并或删除备份/重复副本中的锚点，使整个工作区内每种 memoryType **仅一处**锚点。

契约以本技能正文为准。
