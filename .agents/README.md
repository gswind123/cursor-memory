# `.agents/` — 用户全局 Skills 源目录

本目录下的 **`skills/`** 子目录可同步到 Cursor 用户全局 Skills 路径：

- Windows：`%USERPROFILE%\.agents\skills`
- 类 Unix：`~/.agents/skills`

**必读**

- **`search-memory-storage`** — 维护「候选基准目录列表」与 root 解析算法（flow / stack 共用）。
- **`use-flow-memory`** / **`archive-flow-memory`**、**`use-stack-memory`** / **`archive-stack-memory`** — 读写流程；各目录内 **`reference.md`** 为目录契约（不含 root 列表）。
