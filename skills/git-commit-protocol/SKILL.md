---
name: git-commit-protocol
description: Git 提交规范。当用户要求提交代码、创建 git commit、或使用 /git-commit-protocol 命令时激活此技能。遵循安全的 git 操作流程，包括状态检查、变更分析、提交消息起草和执行提交。
---

# Git 提交规范

## 基本原则

只在用户明确要求时创建提交。如果不确定，先询问用户。

## Git 安全协议

当用户要求创建新的 git 提交时，请严格遵循以下步骤：

### 禁止的操作

- **永远不要**更新 git 配置
- **永远不要**运行破坏性的 git 命令（push --force, reset --hard, checkout ., restore ., clean -f, branch -D），除非用户明确要求这些操作
- **永远不要**跳过 hooks（--no-verify, --no-gpg-sign 等），除非用户明确要求
- **永远不要**强制推送到 main/master 分支，如果用户要求这样做请警告用户
- **关键**：始终创建新的提交而不是修改提交（amend），除非用户明确要求 git amend
- 在暂存文件时，优先按名称添加特定文件，而不是使用 "git add -A" 或 "git add ."
- **永远不要**提交更改，除非用户明确要求

## 提交流程

### 1. 了解当前状态

并行运行以下命令：

- `git status` 查看所有未跟踪的文件（不要使用 -uall 标志）
- `git diff` 查看已暂存和未暂存的更改
- `git log` 查看最近的提交消息风格

### 2. 分析更改并起草提交消息

- 总结更改的性质（新功能、增强、错误修复、重构等）
- 不要提交可能包含机密信息的文件（.env、credentials.json 等）
- 起草简洁的（1-2 句话）提交消息，重点关注"为什么"而不是"什么"

### 3. 执行提交

- 将相关文件添加到暂存区
- 使用 HEREDOC 格式创建提交，消息以此结尾：
  ```
  Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
  ```
- 提交完成后运行 `git status` 验证成功

## 重要注意事项

- 不要运行额外的命令来读取或探索代码，除了 git bash 命令
- 不要推送到远程仓库，除非用户明确要求
- 不要使用带 -i 标志的 git 命令（如 git rebase -i）
- 不要在 git rebase 命令中使用 --no-edit
- 如果没有要提交的更改，不要创建空提交
- 始终通过 HEREDOC 传递提交消息：

```bash
git commit -m "$(cat <<'EOF'
这里是提交消息。

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
EOF
)"
```
