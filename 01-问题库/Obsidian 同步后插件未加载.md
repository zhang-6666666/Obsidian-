---
title: Obsidian 同步后插件没被加载
date: 2026-11-04
tags:
  - 工具/Obsidian
  - 配置
难度: 简单
解决状态: 已解决
环境: Windows 11 / Obsidian 桌面端
---

# 症状

从 GitHub 拉取了完整笔记库，`.obsidian/plugins/` 下插件文件齐全（manifest.json、main.js 都在），
但 Obsidian 里第三方插件没生效，或者插件列表里看不到。

# 原因

按可能性从高到低：

1. **受限模式（Restricted Mode）开启** —— 最优先排查。Obsidian 默认在陌生仓库里打开受限模式，
   此时即使插件文件存在也不会加载。
2. **Obsidian 启动时缓存了仓库状态** —— 插件文件是在 Obsidian 运行期间被 Git 写进来的，
   需要重启才能识别。
3. **`community-plugins.json` 里没写插件 id** —— 文件在但没登记为"已启用"。

# 解决方法

## 步骤 1：关闭受限模式

设置 → 第三方插件（Community plugins）→ 如果有「启用第三方插件 / Turn on community plugins」按钮，点击它。

## 步骤 2：重启 Obsidian

**必须完全退出**，包括右下角托盘图标右键 → 退出。只关窗口不算。
重新打开后检查插件是否出现在「已安装插件」列表。

## 步骤 3：验证清单

```powershell
# 检查插件三件套是否齐全
Get-ChildItem "$env:USERPROFILE\..\path\to\vault\.obsidian\plugins" -Directory | ForEach-Object {
  $ok = (Test-Path "$($_.FullName)\manifest.json") -and (Test-Path "$($_.FullName)\main.js")
  "{0} {1}" -f $_.Name, $(if($ok){"OK"}else{"缺文件"})
}

# 检查启用清单
Get-Content "$env:USERPROFILE\..\path\to\vault\.obsidian\community-plugins.json"
```

`manifest.json` 里的 `id` 必须出现在 `community-plugins.json` 数组中。

## 步骤 4：手动启用

设置 → 第三方插件 → 找到插件 → 点开关打开。

# 踩坑记录

- ❌ 以为是 Git 没同步插件 → 实际用 `git ls-files .obsidian/plugins` 一查，文件全在
- ❌ 以为要重装插件 → 不需要，文件已在正确位置
- ⚠️ 注意版本覆盖：远程仓库的插件版本会**覆盖**本地同名插件（例如本地 v2.42.0 被远程 v2.38.3 覆盖）。
  想用新版需在插件市场手动更新。

# 相关知识

- [[问题库使用说明]]

# 参考

- [Obsidian 官方文档：第三方插件](https://help.obsidian.md/Community+plugins)
