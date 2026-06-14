
> 面向零基础小白，每个命令都配有解释和名词说明。

---

## 一、前置概念：Git 到底是什么？

**Git** 是一个**版本控制系统**，简单说就是帮你**记录文件每一次修改**的工具。你可以把它理解成游戏的「存档」功能——什么时候想回到之前的某个状态，一键就能回去。

### 核心名词解释

| 名词                         | 通俗解释                                                          |
| -------------------------- | ------------------------------------------------------------- |
| **仓库（Repository）**         | 被 Git 管理的项目文件夹。里面有一个隐藏的 `.git` 文件夹，存放所有版本记录。                  |
| **工作区（Working Directory）** | 就是你在电脑上看到的项目文件夹，你在里面改代码、写文档。                                  |
| **暂存区（Staging Area）**      | 一个"购物车"。你改了很多文件，但不是所有都要存——先把要存的放进购物车，再一起结账（提交）。               |
| **提交（Commit）**             | 一次存档。每次 commit 都会生成一个唯一的 ID，以后可以通过这个 ID 找回这次存档的状态。            |
| **分支（Branch）**             | 一条独立的开发线。好比你在主线剧情之外开了个支线任务，做好了再合并回主线。默认分支叫 `main` 或 `master`。 |
| **远程仓库（Remote）**           | 存放在服务器上的仓库（如 GitHub、Gitee），用来和队友共享代码。                         |
| **HEAD**                   | 一个指针，指向你当前所在的分支的最新 commit。可以理解为"我在哪"。                         |

### 三个区域的关系

```
工作区  ──git add──▶  暂存区  ──git commit──▶  仓库（版本库）
 (改文件)            (购物车)                (存档完成)
```

---

## 二、安装与配置

### 2.1 检查是否已安装

```bash
git --version
```

> 如果输出类似 `git version 2.43.0`，说明已安装。否则去 [git-scm.com](https://git-scm.com) 下载安装。

### 2.2 配置用户名和邮箱

每一次 commit 都会记录是谁提交的，所以先要告诉 Git 你是谁：
> user.name和email可以被反复修改

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱@example.com"
```

| 参数 | 含义 |
|------|------|
| `--global` | 全局配置，对本电脑上所有 Git 仓库生效 |
| `user.name` | 你的名字（会出现在提交记录里） |
| `user.email` | 你的邮箱（一般和 GitHub 注册邮箱一致） |

查看当前配置：

```bash
git config --list
```

---

## 三、初始化与基础操作

### 3.1 `git init` — 初始化仓库

进入你的项目文件夹，执行：

```bash
git init
```

> 这会在当前文件夹下创建一个隐藏的 `.git` 目录，从此这个文件夹就是一个 Git 仓库了。

### 3.2 `git status` — 查看当前状态

```bash
git status
```

> 最常用的命令之一。告诉你：哪些文件被修改了、哪些在暂存区、哪些还没被跟踪。**当你不知道接下来该干嘛的时候，先敲 `git status`。**

输出解读：

| 状态提示                            | 含义              |
| ------------------------------- | --------------- |
| `Untracked files`               | 新文件，Git 还没开始跟踪它 |
| `Changes not staged for commit` | 文件已修改，但还没放入暂存区  |
| `Changes to be committed`       | 文件已在暂存区，等待提交    |

### 3.3 `git add` — 添加到暂存区

```bash
# 添加单个文件
git add 文件名.md

# 添加当前目录下所有修改过的文件
git add .

# 添加所有文件（包括删除的文件）
git add -A
```

> 把工作区的修改放入暂存区（购物车）。只有放进暂存区的文件，下次 commit 时才会被存档。

| 参数 | 含义 |
|------|------|
| `.` | 当前目录及子目录下所有改动的文件 |
| `-A` 或 `--all` | 仓库内所有文件（包括删除操作） |

### 3.4 `git commit` — 提交到仓库

```bash
git commit -m "描述你做了什么修改"
```

> 把暂存区的内容正式存档。`-m` 后面跟的是**提交信息**（commit message），用来告诉未来的自己这次做了什么。

**好的提交信息示例：**
- `修复登录页密码验证 bug`
- `添加用户注册功能`
- `更新 README 安装说明`

**建议**：每次 commit 只做一件事，提交信息用中文简明描述即可。

### 3.5 完整工作流演示

```bash
# 1. 写了新文件，看看状态
git status

# 2. 把新文件加入暂存区
git add 新文章.md

# 3. 再看看状态，确认无误
git status

# 4. 提交存档
git commit -m "添加 Git 使用指南文章"

# 5. 查看提交记录
git log
```

---

## 四、查看历史与差异

### 4.1 `git log` — 查看提交历史

```bash
git log
```

> 按时间倒序显示所有 commit 记录，包括作者、时间、提交信息。

常用参数：

```bash
# 简洁模式，一行显示一条 commit
git log --oneline

# 显示最近 3 条
git log -3

# 图形化显示分支路线
git log --oneline --graph --all
```

输出示例：

```
a1b2c3d (HEAD -> main) 添加 Git 使用指南
e4f5g6h 修复登录验证 bug
i7j8k9l 初始化项目
```

| 列 | 含义 |
|----|------|
| `a1b2c3d` | commit 的唯一 ID（哈希值） |
| `(HEAD -> main)` | 当前在 main 分支的最新提交 |
| 后面的文字 | 提交信息 |

### 4.2 `git diff` — 查看具体改了什么

```bash
# 查看工作区和暂存区的差异（还没 git add 的内容）
git diff

# 查看暂存区和上次 commit 的差异（已经 git add 但还没 commit 的内容）
git diff --staged

# 查看两个 commit 之间的差异
git diff commit1的ID commit2的ID
```

> 输出中 `-` 开头的是被删除的行，`+` 开头的是新增的行。这是最有用的排查工具。

---

## 五、分支操作

### 5.1 为什么需要分支？

假设你在写一个新功能，写到一半突然线上出了 bug 要紧急修复。如果没有分支，你只能把写了一半的代码删掉或者硬着头皮改——非常痛苦。

有了分支，你可以：
1. 从主线开一个 `新功能` 分支，安心写功能
2. 紧急 bug 来时，切回 `main` 分支开一个 `修复bug` 分支去修
3. 修完合并回主线，再切回 `新功能` 分支继续写

**各分支互不干扰。**

### 5.2 `git branch` — 查看和创建分支

```bash
# 查看所有本地分支（当前分支前有 * 号）
git branch

# 创建新分支（但不切换过去）
git branch 分支名

# 删除分支（已合并的才能删）
git branch -d 分支名

# 强制删除分支
git branch -D 分支名
```

### 5.3 `git switch` — 切换分支

```bash
# 切换到已有分支
git switch 分支名

# 创建新分支并立即切换过去（最常用）
git switch -c 新分支名
```

> **注意**：`-c` 是 create 的缩写，意为创建并切换。

> **旧命令**：你可能还会看到 `git checkout 分支名` 和 `git checkout -b 新分支名`，功能和 `switch` 一样，是老写法，新版本推荐用 `switch`。

### 5.4 `git merge` — 合并分支

```bash
# 1. 先切换到目标分支（你要把代码合并到哪）
git switch main

# 2. 把另一个分支合并进来
git merge 要合并的分支名
```

> 这会把「要合并的分支」的改动，合并到「当前所在的分支」里。

**合并冲突**：如果两个分支改了同一个文件的同一行，Git 不知道以谁为准，就会产生冲突。你需要手动打开那个文件，选择保留哪些内容，然后重新 `add` + `commit`。

### 5.5 分支操作完整演示

```bash
# 从 main 开一个新分支做功能
git switch -c feature-login

# 写了一堆代码...
git add .
git commit -m "完成登录功能"

# 切回 main，准备合并
git switch main

# 合并功能分支
git merge feature-login

# 功能分支没用了，删掉
git branch -d feature-login
```

---

## 六、远程仓库（GitHub / Gitee）

### 6.1 `git remote add` — 关联远程仓库

先在 GitHub / Gitee 上创建一个空仓库（不要勾选 "Add a README file"），拿到仓库地址，然后：

```bash
git remote add origin 你的远程仓库地址
```

| 参数 | 含义 |
|------|------|
| `origin` | 远程仓库的**别名**，习惯上叫 origin（你也可以取别的名字） |
| 仓库地址 | 形如 `https://github.com/用户名/仓库名.git` 或 `git@github.com:用户名/仓库名.git`（SSH） |

查看已关联的远程仓库：

```bash
git remote -v
```

### 6.2 `git push` — 推送到远程

```bash
# 推送当前分支到远程
git push origin 分支名

# 首次推送（把本地分支和远程分支关联起来）
git push -u origin main
```

> `-u` 是 `--set-upstream` 的缩写，关联后以后直接敲 `git push` 就行，不用每次都写完整的。

| 参数 | 含义 |
|------|------|
| `origin` | 要推送到哪个远程仓库 |
| `main` | 推送哪个分支 |

### 6.3 `git pull` — 从远程拉取更新

```bash
git pull
```

> 别人推送了新的代码到远程仓库，你用这个命令把最新代码拉到本地。它实际上是 `git fetch`（获取）+ `git merge`（合并）的组合。

### 6.4 `git clone` — 克隆远程仓库到本地

```bash
git clone 远程仓库地址
```

> 把服务器上的整个项目下载到本地，自带 `.git` 目录和所有版本记录。拿到新电脑或者加入新项目时的第一步。

```bash
# 克隆并指定本地文件夹名
git clone 远程仓库地址 我的项目
```

### 6.5 远程协作完整流程

```bash
# 场景：你拿到一台新电脑，想继续开发

# 1. 克隆项目
git clone https://github.com/你的用户名/项目名.git

# 2. 进入项目
cd 项目名

# 3. 创建新分支开始工作
git switch -c feature-xxx

# 4. 写代码，提交
git add .
git commit -m "完成 xxx 功能"

# 5. 推送分支到远程
git push -u origin feature-xxx

# 6. 去 GitHub 网页上创建 Pull Request，等队友审核合并

# 7. 合并后，切回 main，拉取最新代码
git switch main
git pull
```

---

## 七、撤销与回退

> ⚠️ **注意**：撤销操作有些是**不可逆**的，操作前请确认清楚！

### 7.1 `git restore` — 撤销工作区修改

```bash
# 撤销某个文件的修改（回到上次 commit 的状态）
git restore 文件名

# 撤销所有文件的修改
git restore .
```

> 比如你改了一个文件改乱了，想放弃所有修改回到最初的样子，就用这个。

```bash
# 把文件从暂存区撤回到工作区（取消 git add）
git restore --staged 文件名
```

### 7.2 `git reset` — 回退版本

```bash
# 回退到上一个 commit，修改保留在工作区
git reset HEAD~1

# 回退到上一个 commit，修改保留在暂存区
git reset --soft HEAD~1

# 回退到上一个 commit，彻底丢弃所有修改（危险！）
git reset --hard HEAD~1

# 回退到指定 commit
git reset --hard commit的ID
```

| 模式 | 工作区内容 | 暂存区内容 | 说明 |
|------|-----------|-----------|------|
| `--soft` | ✅ 保留 | ✅ 保留 | 只移动 HEAD，代码不变。适合"commit 写错了，想重新写" |
| 默认（不加参数） | ✅ 保留 | ❌ 清空 | 修改回到工作区，需要重新 add |
| `--hard` | ❌ 删除 | ❌ 清空 | **彻底清空**，无法恢复。使用前务必确认！ |

| 写法 | 含义 |
|------|------|
| `HEAD~1` | 上一个 commit |
| `HEAD~3` | 往前数第 3 个 commit |
| `a1b2c3d` | 指定的 commit ID |

> 如果你已经把错误 commit 推送到远程了，回退后需要用 `git push --force` 强制推送（**团队协作时慎用！**）。

---

## 八、常用场景速查表

| 我想做什么 | 命令 |
|-----------|------|
| 初始化本地仓库 | `git init` |
| 看看现在什么状态 | `git status` |
| 把文件加入暂存区 | `git add 文件名` 或 `git add .` |
| 提交存档 | `git commit -m "描述"` |
| 查看提交历史 | `git log --oneline` |
| 创建并切换到新分支 | `git switch -c 分支名` |
| 切换到已有分支 | `git switch 分支名` |
| 查看所有分支 | `git branch` |
| 合并分支 | `git switch main` → `git merge 分支名` |
| 关联远程仓库 | `git remote add origin 地址` |
| 推送到远程 | `git push -u origin main` |
| 拉取远程更新 | `git pull` |
| 克隆远程仓库 | `git clone 地址` |
| 撤销文件修改 | `git restore 文件名` |
| 取消 git add | `git restore --staged 文件名` |
| 回退到上一个版本 | `git reset HEAD~1` |
| 回退并彻底删除修改 | `git reset --hard HEAD~1` |
| 查看两个版本的差异 | `git diff` |
| 暂存当前工作（临时切分支） | `git stash` → `git stash pop` |

---

## 九、进阶技巧

### 9.1 `git stash` — 临时保存工作现场

你在开发新功能，突然要切分支修 bug，但又不想 commit 写了一半的代码：

```bash
# 把当前所有未提交的修改暂存起来
git stash

# 切分支修完 bug 后，回到这里恢复
git stash pop
```

### 9.2 `.gitignore` — 忽略不需要跟踪的文件

在项目根目录创建 `.gitignore` 文件：

```
# 忽略 node_modules 文件夹
node_modules/

# 忽略所有 .log 文件
*.log

# 忽略 .env 配置文件（防止密码泄露）
.env
```

> 像 `node_modules`、编译产物、系统缓存文件、密码配置文件都不应该提交到仓库，用 `.gitignore` 告诉 Git 忽略它们。

### 9.3 SSH 方式连接 GitHub（免密码）

每次 push 都输密码很麻烦，可以配置 SSH：

```bash
# 1. 生成 SSH 密钥（一路回车即可）
ssh-keygen -t ed25519 -C "你的邮箱"

# 2. 复制公钥
cat ~/.ssh/id_ed25519.pub

# 3. 把输出的内容粘贴到 GitHub → Settings → SSH and GPG keys → New SSH key

# 4. 测试连接
ssh -T git@github.com
```

之后 clone 时用 SSH 地址（`git@github.com:用户名/仓库名.git`）就行了。

---

## 十、小结

| 阶段 | 核心命令 |
|------|---------|
| 配置 | `git config` |
| 本地开发 | `git init` → `git add` → `git commit` |
| 分支协作 | `git switch -c` → `git merge` |
| 远程同步 | `git clone` → `git pull` → `git push` |
| 救火 | `git status` → `git restore` → `git reset` |

记住一个原则：**不知道现在什么情况时，先敲 `git status`。**

---

> 最后更新：2026-06-14
