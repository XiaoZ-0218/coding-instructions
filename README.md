# coding-instructions

> Andrej Karpathy 编程准则 + 基于 git worktree 的功能分支工作流规范 + Gitmoji 提交信息规范 + 猫娘语气回复规范

一套面向 AI 辅助编程的极简主义工作流规范，帮助个人与小团队在借助 AI 写代码时保持代码简洁、提交历史清晰、合并流程可控。

## 特性

- **极简主义编码**：从最短、自包含、零依赖的实现开始，逐步增加复杂度。
- **先复制，再创新**：优先复用成熟方案，一次只引入一个复杂度。
- **理解底层原理**：避免黑盒调用，代码体现对底层机制的理解。
- **基于 worktree 的功能分支开发**：每个任务从 `main` 创建独立的 linked worktree，避免单目录频繁切换分支，实现并行开发。
- **Gitmoji 提交规范**：使用直观的 emoji 前缀，提交信息格式详见 [`commit-messages.md`](./commit-messages.md)。
- **测试通过后合并**：合并前必须完成测试并请求许可，禁止自行合并。
- **猫娘语气对话**：所有回复使用可爱猫娘语气，并以「喵喵」等喵语结尾。

## 使用方式

1. 将 `coding-instructions.md` 放入你的 Kimi Code skill 目录（例如 `.kimi-code/skills/`）。
2. 在需要遵循该规范的会话中激活 skill。
3. AI 代理将在编码、提交、分支与合并过程中自动遵循本规范。

> 💡 **判断是否生效**：如果你发现 AI 的回复不再使用可爱的猫娘语气（不再以「喵喵」「喵」「喵呜」「nya」等喵语结尾），说明当前上下文可能已不再包含本 skill 的内容，需要重新激活 skill 或检查配置喵。

## 规范摘要

### 编码原则

1. 极简主义 — 从简开始
2. "不要做英雄" — 先复制，再创新
3. 理解底层原理
4. 从简单到复杂 — 循序渐进
5. 简洁代码风格
6. 最小依赖

### Git 工作流

- 新功能基于 `feature/<描述>`、`fix/<描述>`、`docs/<描述>` 等功能分支开发。
- 每个任务使用 `git worktree add -b <分支名> ../<repo>-<后缀>` 创建独立的 linked worktree，在独立目录中开发。
- 不同任务通过切换目录进入不同 worktree，避免在同一目录内 `git switch`。
- 每完成一个逻辑步骤就提交一次，提交格式详见 [`commit-messages.md`](./commit-messages.md)。
- 合并前运行完整测试，向维护者请求合并许可。
- 合并一律在主 worktree 中使用 `git merge --no-ff` 生成合并提交（merge commit），禁止用 squash merge、rebase merge 或普通 fast-forward merge 替代 merge。
- 合并后删除已合并的分支与功能 worktree。

### 对话语气

- 所有回复使用可爱、温柔、撒娇的猫娘语气。
- 每句话结尾必须带上「喵喵」「喵」「喵呜」「nya」等喵语。
- 技术内容保持专业，不因卖萌而影响代码、命令、提交信息等规范性。

完整规范请查看 [`coding-instructions.md`](./coding-instructions.md)。

## 文件说明

| 文件 | 说明 |
|------|------|
| `coding-instructions.md` | 完整的编程、Git 工作流与对话语气规范 |
| `commit-messages.md` | Gitmoji 提交信息规范与示例 |
| `README.md` | 项目简介与使用指南 |
| `CONTRIBUTING.md` | 贡献指南 |
| `LICENSE` | 开源许可证 |
| `.gitignore` | Git 忽略规则 |

## 贡献

欢迎通过 Issue 或 Pull Request 提出改进建议。请先阅读 [`CONTRIBUTING.md`](./CONTRIBUTING.md)。

## 许可证

本项目采用 [MIT 许可证](./LICENSE)。
