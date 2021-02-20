---
title: windiws terminal 配置记录
tags:
  - terminal
  - 配置
categories:
  - 记录
toc: false
date: 2021-02-20 17:02:36
---

# windiws terminal 配置备份

> 系统版本 win10 1909 10.0.18363.778

- 资料1：Windows Terminal 美化实例 https://zhuanlan.zhihu.com/p/76436374
- 资料2：PowerShell主题设置 https://zhuanlan.zhihu.com/p/125515761

> 关于字体

- Fira Code
- Source Code Pro
- Jetbrains Mono
- 更纱黑体
- 筑紫A丸（阅读字体）
- Menlo （ Mac下发现的，还挺好看 ）

前三种都是英文字体

`Jetbrains Mono, Sarasa Term SC, Fira Code, Source Code Pro, Consolas, 'Courier New', monospace`

## 安装

- oh-my-posh
- posh-git
- Get-ChildItemColor

```powershell
#所以先以管理员方式打开 PowerShell，然后分别运行下面的两条命令：
Install-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force
Set-PSRepository -Name PSGallery -InstallationPolicy Trusted
```

```powershell
#在普通 PowerShell 中 使用下面的命令安装 oh-my-posh 、 posh-git 和 Get-ChildItemColor ：
Install-Module -AllowClobber posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
Install-Module -AllowClobber Get-ChildItemColor -Scope CurrentUser
#其实直接在管理员模式下运行上面命令（去掉末尾的-Scope CurrentUser ）还会省去很多麻烦
```

## 配置

Microsoft.PowerShell_profile.ps1

- 通过该命令获取文件路径
- `if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force } `

```powershell
# 在打开 PowerShell 时导入模块
Import-Module Get-ChildItemColor
# 通过别名的方式将 l 和 ls 设置为 Get-ChildItemColor 相关输出以进行着色
Set-Alias l Get-ChildItem -option AllScope
Set-Alias ls Get-ChildItemColorFormatWide -option AllScope
# 导入另外两个模块
Import-Module posh-git
Import-Module oh-my-posh
# 选择主题（可以在命令行中输入 Set-Theme 加 tab 来查看可用主题名称）
Set-Theme Sorin
```

window terminal
profiles.json

```javascript
// To view the default settings, hold "alt" while clicking on the "Settings" button.
// For documentation on these settings, see: https://aka.ms/terminal-documentation
{
  "$schema": "https://aka.ms/terminal-profiles-schema",
  "defaultProfile": "{1d4e097e-fe87-4164-97d7-3ca794c316fd}",
  "initialCols": 80,
  "initialRows": 30,
  "profiles": {
    "defaults": {
      // Put settings here that you want to apply to all profiles
      "acrylicOpacity": 0.85,
      "useAcrylic": true,
      "fontFace": "Sarasa Term SC",
      "cursorShape": "vintage",
      "colorScheme": "Molokai"
    },
    "list": [
      {
        // Git bash profile
        "guid" : "{1d4e097e-fe87-4164-97d7-3ca794c316fd}",
        "hidden": false,
        "name": "Git bash",
        "commandline": "C:\\Program Files\\Git\\bin\\bash.exe",
        "icon":"https://blog.walterlv.com/static/posts/2019-07-02-10-22-00.png",
      },
      {
        // Make changes here to the powershell.exe profile
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "name": "Windows PowerShell",
        "commandline": "powershell.exe",
        "hidden": false,
      },
      {
        // Make changes here to the cmd.exe profile
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "name": "cmd",
        "commandline": "cmd.exe",
        "hidden": false,
        "colorScheme": "3024 Day",
        "cursorColor": "#657B83"
      },
      {
          "guid": "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
          "hidden": false,
          "name": "Debian",
          "source": "Windows.Terminal.Wsl"
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": false,
        "name": "Azure Cloud Shell",
        "source": "Windows.Terminal.Azure"
      }
    ]
  },
  // Add custom color schemes to this array
  "schemes": [
    {
      "name": "3024 Day",
      "black": "#090300",
      "red": "#db2d20",
      "green": "#01a252",
      "yellow": "#fded02",
      "blue": "#01a0e4",
      "purple": "#a16a94",
      "cyan": "#b5e4f4",
      "white": "#a5a2a2",
      "brightBlack": "#5c5855",
      "brightRed": "#e8bbd0",
      "brightGreen": "#3a3432",
      "brightYellow": "#4a4543",
      "brightBlue": "#807d7c",
      "brightPurple": "#d6d5d4",
      "brightCyan": "#cdab53",
      "brightWhite": "#f7f7f7",
      "background": "#f7f7f7",
      "foreground": "#4a4543"
    },
    {
      "name": "Atom",
      "black": "#000000",
      "red": "#fd5ff1",
      "green": "#87c38a",
      "yellow": "#ffd7b1",
      "blue": "#85befd",
      "purple": "#b9b6fc",
      "cyan": "#85befd",
      "white": "#e0e0e0",
      "brightBlack": "#000000",
      "brightRed": "#fd5ff1",
      "brightGreen": "#94fa36",
      "brightYellow": "#f5ffa8",
      "brightBlue": "#96cbfe",
      "brightPurple": "#b9b6fc",
      "brightCyan": "#85befd",
      "brightWhite": "#e0e0e0",
      "background": "#161719",
      "foreground": "#c5c8c6"
    },
    {
      "name": "Molokai",
      "black": "#121212",
      "red": "#fa2573",
      "green": "#98e123",
      "yellow": "#dfd460",
      "blue": "#1080d0",
      "purple": "#8700ff",
      "cyan": "#43a8d0",
      "white": "#bbbbbb",
      "brightBlack": "#bbbbbb",
      "brightRed": "#f6669d",
      "brightGreen": "#b1e05f",
      "brightYellow": "#fff26d",
      "brightBlue": "#00afff",
      "brightPurple": "#af87ff",
      "brightCyan": "#51ceff",
      "brightWhite": "#ffffff",
      "background": "#121212",
      "foreground": "#bbbbbb"
    }
  ],
  // Add any keybinding overrides to this array.
  // To unbind a default keybinding, set the command to "unbound"
  "keybindings": [
    // Copy and paste are bound to Ctrl+Shift+C and Ctrl+Shift+V in your defaults.json.
    // These two lines additionally bind them to Ctrl+C and Ctrl+V.
    // To learn more about selection, visit https://aka.ms/terminal-selection
    { "command": {"action": "copy", "singleLine": false }, "keys": "ctrl+c" },
    { "command": "paste", "keys": "ctrl+v" },

    // Press Ctrl+Shift+F to open the search box
    { "command": "find", "keys": "ctrl+shift+f" },

    // Press Alt+Shift+D to open a new pane.
    // - "split": "auto" makes this pane open in the direction that provides the most surface area.
    // - "splitMode": "duplicate" makes the new pane use the focused pane's profile.
    // To learn more about panes, visit https://aka.ms/terminal-panes
    { "command": { "action": "splitPane", "split": "auto", "splitMode": "duplicate" }, "keys": "alt+shift+d" }
  ]
}
```

效果预览：powershell

![](https://ae01.alicdn.com/kf/H9dc748184724457a9c38597aad6cebbby.jpg)

```
![](https://www.htm.fun/image/5e982dc33ebcb.jpg)
![](https://ae01.alicdn.com/kf/H9dc748184724457a9c38597aad6cebbby.jpg)
![](https://graph.baidu.com/resource/1220af72b7ebacacdf6d901587031498.jpg)
```

效果预览：cmd

![](https://ae01.alicdn.com/kf/Hff5e4581d4d0457ca41e5c713f19c30ef.jpg)

```
![](https://www.htm.fun/image/5e982dbb64fa5.jpg)
![](https://ae01.alicdn.com/kf/Hff5e4581d4d0457ca41e5c713f19c30ef.jpg)
![](https://graph.baidu.com/resource/122e86e2b33dc23861d6101587031490.jpg)
```

