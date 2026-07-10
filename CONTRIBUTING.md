# 贡献指南

感谢你对 `coding-instructions` 的关注！本规范是面向 AI 辅助编程的工作流约定，欢迎通过 Issue 或 Pull Request 参与改进。

## 如何贡献

### 1. 提交 Issue

如果你发现：

- 规范描述存在歧义或错误
- 缺少某种常见场景的约定
- 示例不够清晰

请先搜索是否已有相关 Issue，如果没有，请新建一个 Issue，描述清楚问题或建议。

### 2. 提交 Pull Request

1. Fork 本仓库并 clone 到本地。
2. 在本地仓库同步主分支：
   ```bash
   git pull origin main
   ```
3. 从主分支切出功能分支：
   - 新增规范内容：
     ```bash
     git checkout -b feature/<简短描述> main
     ```
   - 修复问题：
     ```bash
     git checkout -b fix/<简短描述> main
     ```
   - 文档改进：
     ```bash
     git checkout -b docs/<简短描述> main
     ```
   
   > 如果你是通过 `git worktree` 维护本仓库，请从对应 worktree 的上游分支切出功能分支，并在该 worktree 内完成开发。

4. 在功能分支上进行修改，每次只做一个逻辑改动。
5. 提交时遵循本项目的 Gitmoji 提交规范，详见 [`commit-messages.md`](./commit-messages.md)。
6. 确保 Markdown 格式正确、链接可用。
7. 向 `main` 分支发起 Pull Request，描述改动原因与影响范围。
8. PR 合并后，删除已合并的功能分支：
   ```bash
   git branch -d <分支名>
   ```

## 规范修改原则

- 保持简洁：宁可拆分多条规则，也不要把多种场景硬塞进一条。
- 保持可执行：每条规范都应能被 AI 代理或开发者直接执行。
- 保持一致：新增内容应与现有 Andrej Karpathy 准则和 Git 工作流风格保持一致。
- 提供示例：抽象的约定最好配上具体示例。

## 代码风格

- 使用中文编写规范正文。
- Markdown 标题层级清晰，避免过深的嵌套。
- 列表项保持一致的标点与格式。

## 行为准则

请保持友善、尊重与建设性。不同团队的工作流各有差异，本规范的目标是提炼一套通用且可落地的约定。
