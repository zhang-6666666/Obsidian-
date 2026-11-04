---
title: Git 推送到 GitHub 极慢 / 梯子开关都不同步
date: 2026-11-04
updated: 2026-11-04
tags:
  - 工具/Git
  - 配置
  - 性能
难度: 中等
解决状态: 已解决
环境: Windows 11 / Git 2.45.1 / OpenSSH 9.5p2 / Clash 代理 127.0.0.1:7897
---

# 症状

两个现象，其实是同一个原因：

**现象 A —— 极慢**

`git fetch` / `git push` 卡几分钟只走到 20%：

```
Receiving objects:  20% (32/160), 1.16 MiB | 26.00 KiB/s
```

但同一时间浏览器访问 GitHub 秒开。

**现象 B —— 关梯子就报错**

给 SSH 配上代理后，一关梯子就推不上去：

```
connect: 由于目标计算机积极拒绝，无法连接。
fatal: Could not read from remote repository.
```

因为 `ProxyCommand` 硬编码了 `127.0.0.1:7897`，梯子退出后端口没人监听，
SSH **不会自动回退直连**，而是直接失败。

# 原因

## 根因 1：SSH 不读 Windows 系统代理

- 浏览器、`Invoke-WebRequest` 等会读取系统代理（`HKCU:\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ProxyServer`）
- 而 `git` 走 SSH（`git@github.com:...`）时，由 `ssh.exe` **直接建 TCP 连接**到 `github.com:22`
- 于是 SSH 流量**绕过代理直连 GitHub**，被限速到 20~30 KB/s

对比实测：

| 方式 | 耗时 |
|---|---|
| HTTPS 走代理访问 GitHub API | **0.4 秒** |
| SSH 直连 `git fetch`（被限速时） | **卡 2 分钟未完成** |

## 根因 2：静态代理配置没有容错

`ProxyCommand` 是无条件的。只要写了它，每次连接都必须先连上代理端口，
代理不在就整个失败——这是我一开始没考虑到的情况。

## 重要事实：直连本身通常没问题

补测发现：**同一台机器、同样的网络，直连 GitHub 很多时候只要 5 秒左右。**

| 测试项 | 走代理 | **直连** |
|---|---|---|
| `git fetch` | 28 秒 | **4.9 秒** |
| `git push` | 5.5 秒 | **5.5 秒** |
| HTTPS API | 0.4 秒 | 0.4 秒 |

所以 26 KB/s 那次是**当时的路由波动**，不是常态。
结论：不能假设"必须走代理"，也不能假设"直连一定快"——**两者都要能工作**。

# 解决方法

## 方案：自适应代理（自动判断梯子开关）

需要两个文件配合。

### 文件 1：端口检测脚本

`C:\Users\<用户名>\.ssh\check-proxy.cmd`

```cmd
@echo off
powershell -NoProfile -ExecutionPolicy Bypass -Command "if(Test-NetConnection -ComputerName 127.0.0.1 -Port 7897 -InformationLevel Quiet -WarningAction SilentlyContinue){exit 0}else{exit 1}"
```

- 端口可连 → `exit 0`（条件成立，启用代理）
- 端口不通 → `exit 1`（条件不成立，跳过代理）

### 文件 2：SSH 配置

`C:\Users\<用户名>\.ssh\config`

```ssh
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
    ConnectTimeout 15
    ServerAliveInterval 30
    ServerAliveCountMax 3

# 仅当 7897 端口可达时，才启用代理
Match host github.com exec "C:/Users/31744/.ssh/check-proxy.cmd"
    ProxyCommand "C:/Program Files/Git/mingw64/bin/connect.exe" -H 127.0.0.1:7897 %h %p

Host *
    ServerAliveInterval 30
```

### 工作原理

每次连接 GitHub 时：

```
SSH 启动
  └─ 执行 Match exec 条件：运行 check-proxy.cmd
       ├─ 7897 端口可达？ ── 是 ──> 应用 ProxyCommand，走代理
       └─ 7897 端口可达？ ── 否 ──> 跳过 ProxyCommand，直连 github.com:22
```

### 两种场景的实测结果

| 场景 | 检测结果 | SSH 表现 | 耗时 |
|---|---|---|---|
| 梯子开着 | 端口可达 → 走代理 | ✅ 认证成功 | 4.3 秒 |
| 梯子关了 | 端口不通 → 直连 | ✅ 认证成功 | 5.9 秒 |
| Git 实际操作 | — | ✅ `git fetch` 成功 | 5.3 秒 |

**关键前提**：实测 `connect.exe` 在代理端口不通时 **2.1 秒就快速失败**，
不会卡住。所以即使检测判断有偏差（检测瞬间梯子刚好断），
最坏也只是 2 秒后报错一次，不会卡几分钟。

## 验证方法

```powershell
# 1. 看端口状态
Test-NetConnection 127.0.0.1 -Port 7897 -InformationLevel Quiet

# 2. 测 SSH 认证
ssh -T git@github.com
# 返回 "Hi <用户名>! You've successfully authenticated..." 即成功
# 注意：exit code 1 是正常的，不代表失败

# 3. 端到端测试
cd E:\Brain
git fetch origin
```

# 踩坑记录

## 关于限速的判断

- ❌ 以为是仓库太大 → 实际仓库才 51 MB，`ls-remote` 7 秒就返回
- ❌ 以为是网络抖动重试多次 → 每次都是 26 KB/s **稳定**限速，说明是路由问题不是波动
- ❌ 以为是 SSH 本身有问题 → `ssh -T` 认证一直正常，只是数据传输慢

## 关于 connect.exe

- ❌ 直接把 `connect.exe` 写进 `ProxyCommand` → 找不到命令，**它不在 PATH 里**，必须写绝对路径
  （通常在 `C:\Program Files\Git\mingw64\bin\connect.exe`）
- `-H` = HTTP 代理，`-S` = SOCKS5 代理，别混

## 关于 Match exec（踩坑最多的一环）

`Match exec` 的引号处理非常麻烦，尝试过但**失败**的做法：

- ❌ 把 PowerShell 命令直接内联进 `Match exec "..."`
  → 嵌套引号 `\"...\"` 被 SSH 的配置解析器吃掉，报错 `\ : The term '\' is not recognized`
- ❌ 用 `exit (... -eq $false)` 这种写法
  → `exit` 后面不能直接接比较表达式
- ❌ 检测脚本用 `.ps1` 但只写相对路径
  → `-File` 参数找不到文件，SSH 直接报错而不是回退直连
- ❌ 为了模拟"梯子关闭"把 `config` 里的 `7897` 全局替换
  → **把 ProxyCommand 的端口也改了**，测出来的是"代理端口错"而不是"梯子关闭"，
  白白浪费一轮。**改配置要精确定位，不能用全局替换**

✅ 最终做法：**把检测逻辑放进独立 `.cmd` 文件，用绝对路径调用**，规避所有引号问题。

## 关于"关梯子"的场景

- ❌ 以为配了代理就一劳永逸 → 梯子一关 SSH 直接失败，**不会自动回退**
- ⚠️ 曾考虑直接删掉代理配置（因为直连也快）→ 但用户在特定场景下**必须挂梯子**，
  而忘了关梯子是最常见情况。所以不能赌单一方案

# 有关键细节

**梯子换端口要改两处**：

1. `check-proxy.cmd` 里的 `-Port 7897`
2. `config` 里 `ProxyCommand` 的 `-H 127.0.0.1:7897`

只改一处会出现"检测说梯子开着但实际走不通"的诡异现象。

**别删 `check-proxy.cmd`**：删了之后 `Match exec` 找不到脚本，
SSH 会报错而不是回退直连。

# 相关知识

- [[问题库使用说明]]
- 替代方案 A：开代理软件的 **TUN / 虚拟网卡模式**，接管全部 TCP/UDP 流量，
  SSH 自动走代理，**完全不需要改 ssh config**。缺点是个别软件检测不到代理
- 替代方案 B：改用 **HTTPS + Personal Access Token**，HTTPS 天然读系统代理。
  缺点是每次要管理 token
- 国内网络建议：Gitee 作为备用远程仓库

# 参考

- [Git for Windows（自带 connect.exe）](https://gitforwindows.org/)
- [OpenSSH ssh_config Match 指令](https://man.openbsd.org/ssh_config#Match)
