# CosyVoice 项目 Git 推送指南

本指南将详细说明如何将 CosyVoice 项目推送到您自己的 Git 仓库。

## 📋 目录

1. [准备工作](#准备工作)
2. [方法一：推送到全新的 Git 仓库](#方法一推送到全新的-git-仓库)
3. [方法二：推送到已存在的 Git 仓库](#方法二推送到已存在的-git-仓库)
4. [方法三：保留原仓库历史并添加新远程仓库](#方法三保留原仓库历史并添加新远程仓库)
5. [处理 Git 子模块](#处理-git-子模块)
6. [常见问题解决](#常见问题解决)
7. [完整操作示例](#完整操作示例)

---

## 准备工作

### 1. 检查当前 Git 状态

首先，检查项目是否已经是 Git 仓库：

```bash
cd /apps/tools/models/CosyVoice
git status
```

**可能的情况：**

- ✅ **如果显示 Git 信息**：说明已经是 Git 仓库，可以直接添加远程仓库
- ❌ **如果显示 "not a git repository"**：需要先初始化 Git 仓库

### 2. 检查远程仓库配置

如果已经是 Git 仓库，查看当前的远程仓库配置：

```bash
git remote -v
```

这会显示当前的远程仓库地址（通常是 `origin`）。

### 3. 准备您的 Git 仓库地址

在开始之前，您需要：
- 在 GitHub、GitLab、Gitee 等平台创建一个新的仓库
- 获取仓库的 HTTPS 或 SSH 地址，例如：
  - HTTPS: `https://github.com/wyt990/CosyVoice2.git`
  - SSH: `git@github.com:wyt990/CosyVoice2.git`

---

## 方法一：推送到全新的 Git 仓库

**适用场景**：项目还不是 Git 仓库，或者您想创建一个全新的仓库。

### 步骤 1：初始化 Git 仓库（如果尚未初始化）

```bash
cd /apps/tools/models/CosyVoice
git init
```

### 步骤 2：添加所有文件到暂存区

```bash
# 添加所有文件（包括子模块）
git add .

# 或者，如果您想排除某些文件，可以先创建 .gitignore
# 然后使用 git add .
```

### 步骤 3：创建初始提交

```bash
git commit -m "第一次提交"
```

### 步骤 4：添加远程仓库

```bash
# 替换为您的实际仓库地址
git remote add origin https://github.com/wyt990/CosyVoice2.git

# 或者使用 SSH
# git remote add origin git@github.com:wyt990/CosyVoice2.git
```

### 步骤 5：推送到远程仓库

```bash
# 推送到主分支（根据您的 Git 版本，可能是 main 或 master）
git branch -M main  # 如果默认分支是 master，重命名为 main
git push -u origin main
```

**如果遇到错误**，可能需要先拉取远程仓库：

```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

---

## 方法二：推送到已存在的 Git 仓库

**适用场景**：项目已经是 Git 仓库，但想更换或添加新的远程仓库。

### 步骤 1：查看当前远程仓库

```bash
git remote -v
```

### 步骤 2：移除旧的远程仓库（可选）

如果您想完全替换远程仓库：

```bash
git remote remove origin
```

### 步骤 3：添加新的远程仓库

```bash
# 添加新的远程仓库
git remote add origin https://github.com/wyt990/CosyVoice2.git

# 或者，如果您想保留旧的远程仓库，可以使用不同的名称
# git remote add myrepo https://github.com/wyt990/CosyVoice2.git
```

### 步骤 4：推送到新仓库

```bash
# 确保所有更改已提交
git add .
git commit -m "Update: Add GPU selection feature and Chinese documentation"

# 推送到新仓库
git push -u origin main
```

**如果远程仓库已有内容**，可能需要强制推送（谨慎使用）：

```bash
# 方法 1：合并历史
git pull origin main --allow-unrelated-histories
git push -u origin main

# 方法 2：强制推送（会覆盖远程仓库，请谨慎使用）
# git push -u origin main --force
```

---

## 方法三：保留原仓库历史并添加新远程仓库

**适用场景**：想保留原仓库的历史记录，同时推送到自己的仓库。

### 步骤 1：添加新的远程仓库（使用不同的名称）

```bash
# 保留原来的 origin，添加新的远程仓库
git remote add myrepo https://github.com/wyt990/CosyVoice2.git

# 查看所有远程仓库
git remote -v
```

### 步骤 2：推送到新仓库

```bash
git push -u myrepo main
```

这样，您可以：
- 继续从原仓库拉取更新：`git pull origin main`
- 推送到自己的仓库：`git push myrepo main`

---

## 处理 Git 子模块

CosyVoice 项目包含 Git 子模块（`third_party/Matcha-TTS`），需要特殊处理。

### 方法 A：包含子模块内容（推荐用于个人备份）

如果您想将子模块的内容直接包含在仓库中：

```bash
# 1. 确保子模块已初始化
git submodule update --init --recursive

# 2. 移除子模块的 .git 目录（使其成为普通目录）
cd third_party/Matcha-TTS
rm -rf .git
cd ../..

# 3. 添加所有文件（包括子模块内容）
git add third_party/Matcha-TTS
git commit -m "Include Matcha-TTS submodule content"

# 4. 推送到远程仓库
git push -u origin main
```

### 方法 B：保留子模块引用（推荐用于开发）

如果您想保留子模块的 Git 引用：

```bash
# 1. 确保子模块已初始化
git submodule update --init --recursive

# 2. 提交子模块引用
git add .gitmodules third_party/Matcha-TTS
git commit -m "Add submodule reference"

# 3. 推送到远程仓库
git push -u origin main

# 4. 推送子模块内容到远程仓库（如果需要）
cd third_party/Matcha-TTS
git push <submodule-remote-url> <branch>
```

**注意**：如果使用子模块，其他人在克隆您的仓库后需要运行：

```bash
git submodule update --init --recursive
```

---

## 常见问题解决

### 问题 1：推送时提示 "remote origin already exists"

**解决方案**：

```bash
# 查看现有远程仓库
git remote -v

# 移除旧的远程仓库
git remote remove origin

# 添加新的远程仓库
git remote add origin https://github.com/wyt990/CosyVoice2.git
```

### 问题 2：推送时提示 "refusing to merge unrelated histories"

**解决方案**：

```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### 问题 3：推送时提示 "authentication failed"

**解决方案**：

**使用 HTTPS：**
```bash
# 使用个人访问令牌（Personal Access Token）
# 在 GitHub/GitLab 设置中生成令牌，然后使用令牌作为密码
git remote set-url origin https://<token>@github.com/wyt990/CosyVoice2.git
```

**使用 SSH：**
```bash
# 1. 生成 SSH 密钥（如果还没有）
ssh-keygen -t ed25519 -C "your_email@example.com"

# 2. 将公钥添加到 GitHub/GitLab
cat ~/.ssh/id_ed25519.pub
# 复制输出内容，添加到平台的 SSH Keys 设置中

# 3. 使用 SSH 地址
git remote set-url origin git@github.com:wyt990/CosyVoice2.git
```

### 问题 4：文件太大无法推送

**解决方案**：

```bash
# 1. 检查大文件
git ls-files | xargs du -h | sort -h | tail -20

# 2. 使用 Git LFS（Large File Storage）
git lfs install
git lfs track "*.pt"  # 跟踪模型文件
git lfs track "*.onnx"
git add .gitattributes
git commit -m "Add Git LFS tracking for large files"

# 3. 重新添加文件
git add .
git commit -m "Add files with LFS"
git push -u origin main
```

### 问题 5：推送时提示 "submodule not found"

**解决方案**：

```bash
# 确保子模块已初始化
git submodule update --init --recursive

# 如果子模块有问题，可以重新初始化
git submodule deinit -f third_party/Matcha-TTS
git submodule update --init --recursive
```

---

## 完整操作示例

以下是一个完整的操作示例，假设您要在 GitHub 上创建一个新仓库。

### 步骤 1：在 GitHub 上创建新仓库

1. 登录 GitHub
2. 点击右上角的 "+" → "New repository"
3. 填写仓库名称（如：`my-cosyvoice`）
4. 选择 Public 或 Private
5. **不要**勾选 "Initialize this repository with a README"
6. 点击 "Create repository"

### 步骤 2：在本地执行命令

```bash
# 进入项目目录
cd /apps/tools/models/CosyVoice

# 检查 Git 状态
git status

# 如果还不是 Git 仓库，初始化
if [ ! -d .git ]; then
    git init
fi

# 添加所有文件（排除大文件，如果需要）
git add .

# 创建提交
git commit -m "Initial commit: CosyVoice project with GPU selection and Chinese docs"

# 添加远程仓库（替换为您的实际地址）
git remote add origin https://github.com/your-username/my-cosyvoice.git

# 设置主分支名称
git branch -M main

# 推送到远程仓库
git push -u origin main
```

### 步骤 3：验证推送结果

```bash
# 查看远程仓库信息
git remote -v

# 查看提交历史
git log --oneline

# 在浏览器中访问您的 GitHub 仓库，确认文件已上传
```

---

## 后续维护

### 日常更新推送

```bash
# 1. 查看更改
git status

# 2. 添加更改
git add .

# 3. 提交更改
git commit -m "描述您的更改"

# 4. 推送到远程仓库
git push origin main
```

### 从原仓库同步更新

如果您保留了原仓库的远程地址：

```bash
# 添加原仓库作为 upstream（如果还没有）
git remote add upstream https://github.com/FunAudioLLM/CosyVoice.git

# 从原仓库拉取更新
git fetch upstream

# 合并更新
git merge upstream/main

# 推送到自己的仓库
git push origin main
```

### 创建分支进行开发

```bash
# 创建新分支
git checkout -b feature/gpu-selection

# 进行开发...

# 提交更改
git add .
git commit -m "Add GPU selection feature"

# 推送到远程仓库
git push -u origin feature/gpu-selection

# 在 GitHub 上创建 Pull Request 或直接合并
```

---

## 注意事项

1. **敏感信息**：推送前检查是否包含敏感信息（API 密钥、密码等），使用 `.gitignore` 排除
2. **大文件**：模型文件（`.pt`, `.onnx`）可能很大，考虑使用 Git LFS 或排除这些文件
3. **许可证**：确保遵守原项目的许可证（Apache 2.0）
4. **子模块**：如果包含子模块，确保正确处理
5. **备份**：重要数据请做好备份

---

## 快速参考命令

```bash
# 初始化仓库
git init

# 添加远程仓库
git remote add origin <repository-url>

# 查看远程仓库
git remote -v

# 移除远程仓库
git remote remove origin

# 添加文件
git add .

# 提交更改
git commit -m "commit message"

# 推送到远程
git push -u origin main

# 拉取更新
git pull origin main

# 查看状态
git status

# 查看提交历史
git log --oneline
```

---

## 获取帮助

如果遇到问题，可以：

1. 查看 Git 官方文档：https://git-scm.com/doc
2. 查看 GitHub 帮助：https://docs.github.com
3. 查看项目的 FAQ.md 文件
4. 在项目的 Issues 中提问

---

**最后更新**：2025-12-13

