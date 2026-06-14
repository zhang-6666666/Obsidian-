

> 快速翻查用，详细解释见 [[Git 命令使用指南.md]]。

---

## 本地操作

| 我想做什么 | 命令 |
|-----------|------|
| 初始化本地仓库 | `git init` |
| 看看现在什么状态 | `git status` |
| 把文件加入暂存区 | `git add 文件名` 或 `git add .` |
| 提交存档 | `git commit -m "描述"` |
| 查看提交历史 | `git log --oneline` |
| 查看两个版本的差异 | `git diff` |
| 撤销文件修改 | `git restore 文件名` |
| 取消 git add | `git restore --staged 文件名` |
| 回退到上一个版本 | `git reset HEAD~1` |
| 回退并彻底删除修改 | `git reset --hard HEAD~1` |
| 暂存当前工作（临时切分支） | `git stash` → `git stash pop` |

## 分支操作

| 我想做什么 | 命令 |
|-----------|------|
| 创建并切换到新分支 | `git switch -c 分支名` |
| 切换到已有分支 | `git switch 分支名` |
| 查看所有分支 | `git branch` |
| 合并分支 | `git switch main` → `git merge 分支名` |

## 远程仓库

| 我想做什么  | 命令                         |
| ------ | -------------------------- |
| 关联远程仓库 | `git remote add origin 地址` |
| 推送到远程  | `git push -u origin main`  |
| 拉取远程更新 | `git pull`                 |
| 克隆远程仓库 | `git clone 地址`             |

## 配置

| 我想做什么 | 命令 |
|-----------|------|
| 设置用户名 | `git config --global user.name "你的名字"` |
| 设置邮箱 | `git config --global user.email "邮箱@example.com"` |
| 查看当前配置 | `git config --list` |
| 正常显示中文文件名 | `git config --global core.quotePath false` |
| 记住密码（HTTPS） | `git config --global credential.helper cache` |

---

> 最后更新：2026-06-14
