---
title: Git 推送到 GitHub 极慢（26KB/s）
date: 2026-11-04
tags:
  - 工具/Git
  - 配置
  - 性能
难度: 中等
解决状态: 已解决
环境: Windows 11 / Git 2.45.1 / Clash 代理 127.0.0.1:7897
---

# 症状

新电脑上 `git fetch` / `git push` 极慢，卡几分钟只走到 20%：

```
Receiving objects:  20% (32/160), 1.16 MiB | 26.00 KiB/s
```

但同一时间用浏览器访问 GitHub 秒开。

# 原因

**SSH 协议不读 Windows 系统代理设置。**

- 浏览器、`Invoke-WebRequest` 等会读取系统代理（`HKCU:\...\Internet Settings\ProxyServer`）
- 而 `git` 走 SSH（`git@github.com:...`）时，由 `ssh.exe` 直接建 TCP 连接到 `github.com:22`
- 于是 SSH 流量**绕过代理直连 GitHub**，被限速到 20~30 KB/s

对比实测：

| 方式 | 耗时 |
|---|---|
| HTTPS 走代理访问 GitHub API | **0.4 秒** |
| SSH 直连 `git fetch` | **卡 2 分钟未完成** |

# 解决方法

给 SSH 配置代理。编辑 `C:\Users\<用户名>\.ssh\config`：

```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
    ProxyCommand "C:/Program Files/Git/mingw64/bin/connect.exe" -H 127.0.0.1:7897 %h %p
    ServerAliveInterval 30
    ServerAliveCountMax 3
```

关键点：

1. `connect.exe` 是 Git for Windows 自带的 HTTP/SOCKS 代理工具，路径 `<Git安装目录>/mingw64/bin/connect.exe`
2. **必须写绝对路径**，它不在 PATH 里
3. `-H` = HTTP 代理，`-S` = SOCKS5 代理
4. 端口 `7897` 要和代理软件监听端口一致（Clash Verge 默认 7897）

验证：

```powershell
ssh -T git@github.com
# 应返回：Hi <用户名>! You've successfully authenticated...
# （exit code 1 是正常的，不代表失败）
```

**效果**：`git fetch` 从卡死 → 28 秒完成；`git push` 17 秒完成。

# 踩坑记录

- ❌ 以为是仓库太大 → 实际仓库才 51 MB，`ls-remote` 7 秒就返回
- ❌ 以为是网络问题重试多次 → 每次都是 26 KB/s 稳定限速，说明是路由问题不是抖动
- ❌ 一开始把 `connect.exe` 直接写进 `ProxyCommand` → 找不到命令，因为不在 PATH

# 相关知识

- [[问题库使用说明]]
- 替代方案：开代理软件的 **TUN / 虚拟网卡模式**，接管全部流量，SSH 自动走代理，无需改 ssh config
- 国内建议：Gitee 作为备用远程，或 GitHub 用 HTTPS + Personal Access Token

# 参考

- [Git for Windows 自带 connect.exe](https://gitforwindows.org/)
