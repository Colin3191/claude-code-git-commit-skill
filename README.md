# git-commit-protocol

喜欢 Claude Code 的 git commit 提交风格，参考了 Claude Code 内部的 prompt 实现，写了这个 skill，让其他 AI coding 工具也能用同样的方式提交代码。

## 它做了什么

- 遵循安全的 git 操作流程：状态检查 → 变更分析 → 提交消息起草 → 执行提交
- 提交消息简洁，关注"为什么"而不是"什么"
- 自动添加 `Co-Authored-By` 标记
- 禁止危险操作（force push、reset --hard 等），除非你明确要求
- 按文件名精确暂存，而不是无脑 `git add .`

## 使用方式

把 `skills/git-commit-protocol` 目录复制到你的 AI coding 工具对应的 skills 目录下即可。不同工具的配置路径可能不同，按各自的约定放置就行。
