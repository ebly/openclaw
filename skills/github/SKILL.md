---
name: github
description: "GitHub 操作技能。用于管理 GitHub 仓库、创建 issue、提交代码、合并 PR 等操作。适用于：代码管理、协作开发、版本控制。"
metadata: { "openclaw": { "emoji": "🐙", "requires": { "env": ["GITHUB_TOKEN"], "bins": ["gh"] } } }
---

# 🐙 GitHub 操作技能

## 📍 使用场景

✅ **使用此技能：**
- "创建一个新的 GitHub 仓库"
- "查看仓库信息"
- "创建 issue"
- "提交代码"
- "创建 pull request"
- "合并分支"
- "查看仓库状态"
- "管理仓库设置"

---

## 🔑 认证配置

### 获取 GitHub Token

1. 访问：https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 选择权限：
   - `repo` - 仓库权限
   - `issues` - Issue 权限
   - `pull requests` - PR 权限
4. 生成并复制 token

### 设置环境变量

```bash
# Linux/Mac
export GITHUB_TOKEN=your_token_here

# Windows PowerShell
$env:GITHUB_TOKEN = "your_token_here"

# 添加到系统环境变量
[System.Environment]::SetEnvironmentVariable('GITHUB_TOKEN', 'your_token_here', 'User')
```

### 安装 GitHub CLI

```bash
# Windows (使用 winget)
winget install --id GitHub.cli

# Mac (使用 brew)
brew install gh

# Linux
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

### 登录 GitHub

```bash
gh auth login
```

---

## 📋 常用命令

### 仓库管理

#### 创建新仓库
```bash
gh repo create my-repo --public
gh repo create my-repo --private
gh repo create my-repo --source=. --remote=origin
```

#### 查看仓库信息
```bash
gh repo view owner/repo
gh repo view owner/repo --json name,description,stars,forks
```

#### 克隆仓库
```bash
gh repo clone owner/repo
gh repo clone owner/repo my-directory
```

---

### Issue 管理

#### 创建 Issue
```bash
gh issue create --title "Bug: 无法登录" --body "描述详细问题..."
gh issue create --title "Feature request" --body "需求描述..." --label enhancement
```

#### 查看 Issue 列表
```bash
gh issue list
gh issue list --label bug
gh issue list --author username
```

#### 查看特定 Issue
```bash
gh issue view 123
gh issue view 123 --comments
```

#### 关闭 Issue
```bash
gh issue close 123
gh issue close 123 --comment "问题已解决"
```

---

### Pull Request 管理

#### 创建 PR
```bash
gh pr create --title "修复登录问题" --body "详细描述..."
gh pr create --base main --head feature-branch
```

#### 查看 PR 列表
```bash
gh pr list
gh pr list --state open
gh pr list --author username
```

#### 查看特定 PR
```bash
gh pr view 456
gh pr view 456 --comments
```

#### 合并 PR
```bash
gh pr merge 456 --squash
gh pr merge 456 --merge
gh pr merge 456 --rebase
```

---

### 分支管理

#### 创建分支
```bash
git checkout -b feature/new-feature
# 或使用 gh
gh repo sync
git checkout -b feature/new-feature
```

#### 查看分支
```bash
gh repo view --json defaultBranchRef
git branch -a
```

#### 删除分支
```bash
git branch -d branch-name
git push origin --delete branch-name
```

---

### 代码提交

#### 提交更改
```bash
git add .
git commit -m "提交信息"
git push
```

#### 查看提交历史
```bash
gh repo view --json latestCommit
git log --oneline -10
```

#### 查看文件差异
```bash
git diff
git diff branch1 branch2
```

---

## 🎯 典型工作流

### 1. 新功能开发

```bash
# 1. 拉取最新代码
git pull origin main

# 2. 创建新分支
git checkout -b feature/new-feature

# 3. 开发并提交
git add .
git commit -m "feat: 添加新功能"
git push -u origin feature/new-feature

# 4. 创建 PR
gh pr create --title "添加新功能" --body "功能描述..."

# 5. 合并 PR
gh pr merge 456 --merge

# 6. 删除分支
git checkout main
git pull origin main
git branch -d feature/new-feature
git push origin --delete feature/new-feature
```

### 2. Bug 修复

```bash
# 1. 创建修复分支
git checkout -b fix/login-bug

# 2. 修复并提交
git add .
git commit -m "fix: 修复登录问题"
git push -u origin fix/login-bug

# 3. 创建 PR
gh pr create --title "修复登录问题" --body "修复说明..."

# 4. 合并
gh pr merge 456 --squash
```

---

## 📊 仓库信息查询

### 查看仓库统计
```bash
gh repo view owner/repo --json name,description,stargazerCount,forkCount,updatedAt
```

### 查看最近的提交
```bash
gh repo view owner/repo --json latestCommit
```

### 查看仓库活动
```bash
gh repo view owner/repo --json pushedAt,createdAt
```

---

## 🛠️ 高级操作

### 搜索仓库
```bash
gh search repos openclaw --limit 10
gh search repos language:python stars:>100
```

### 搜索 Issues
```bash
gh search issues "bug" --owner owner --repo repo
gh search prs "feature" --state open
```

### 查看 Action 状态
```bash
gh run list
gh run view 123
gh run watch
```

---

## ⚠️ 注意事项

### 安全建议
- ✅ 使用 Personal Access Token 而不是密码
- ✅ 为不同用途创建不同 token
- ✅ 定期轮换 token
- ✅ 使用最小权限原则

### 最佳实践
- ✅ 清晰的 commit message
- ✅ PR 描述详细
- ✅ 代码审查
- ✅ 分支命名规范
- ✅ 保护主要分支

---

## 🌟 GitHub CLI 扩展

### 安装扩展
```bash
gh extension install gh-eco/gh-eco
gh extension install github/gh-copilot
```

### 列出已安装扩展
```bash
gh extension list
```

---

## 📚 相关资源

- GitHub CLI 文档：https://cli.github.com/
- GitHub API 文档：https://docs.github.com/en/rest
- Git 官方文档：https://git-scm.com/doc

---

高效管理代码，轻松协作开发！🐙✨