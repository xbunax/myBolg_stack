---
title: "Spotify beautify"
description: 
date: 2024-04-05T11:35:52+08:00
image: https://raw.githubusercontent.com/xbunax/blogImg/main/202404051305362.png
math: 
toc: true
categories: [
"Spotify",
"Beautify",
]
license: 
hidden: false
comments: true
draft: false
---

# Beautify Spotify Desktop App

在上篇关于Spotify TUI的文章中提到Spotify的桌面应用的UI设计博主本人并不是很喜欢，但是最近偶然发现了`spicetify`这款开源的Spotify美化以及插件管理软件，极大提升了Spotify的使用体验。

***

## Install and Uninstall

如果是Mac和Linux推荐使用包管理器安装在终端输入
```
brew install spicetify-cli
```
或者使用官方编译好的二进制文件
```
curl -fsSL https://raw.githubusercontent.com/spicetify/spicetify-cli/master/install.sh | sh
```

卸载方法如下
```
spicetify restore
rm -rf ~/.spicetify
rm -rf ~/.config/spicetify
```
## Prepare

+ 首先在终端中输入
`
spicetify
`
生成配置文件

+ 如果运行无误，接着要备份一下配置文件
```
spicetify backup apply enable-devtools
```

> 在每次更改`theme`和`color`后要需要执行一下`spicetify apply`以应用。


## Customize

```
.$XDG_config/spicetify
├── Backup
├── CustomApps
├── Extensions
├── Extracted
├── Themes
├── config-xpui.ini
└── spicetify-themes
```
这是`spicetify`配置文件的结构，我们主要修改的就是`config-xpui.ini`这个文件，当然也可以直接通过命令行修改。

### customize theme and color
接着就可以设置Spotify的主题以及配色啦。可以在这里找到官方提供的主题库[`THEME.MD`](https://github.com/spicetify/spicetify-themes/blob/master/THEMES.md)，以及第三方提供的[主题方案](https://spicetify.app/docs/advanced-usage/themes)。

+ 命令行修改即在终端中输入
```
spicetify config current_theme 主题配置 color_scheme 配色方案
spicetify apply
```
+ 配置文件中主要修改这两项
```
current_theme          = 主题
color_scheme           = 配色
```
设置好后同样要用`spicetify apply`

### apply extensions 

目前官方提供的插件数量还较少，可以在[Extensions](https://spicetify.app/docs/advanced-usage/extensions)中找到。

+ 与设置主题类似，可以在命令中自动安装
```
spicetify config extensions 插件名
spicetify apply
```
+ 手动修改配置文件
```
[AdditionalOptions]
...
extensions = 插件名称
```
同样要`spicetify apply`

目前用下来`Full App Display`这款插件还不错，可以全屏显示歌曲信息，还有`Pop-up Lyrics`这款插件可以显示歌词。

***

## Show case

个人感觉`Dribbblish`的`Nord-Dark`和`Gruvbox`配色和主题还不错

![Gruvbox](https://raw.githubusercontent.com/xbunax/blogImg/main/202404051309961.png)

目前我用的是`text`的`Catppuccin Latte`配色

![text](https://raw.githubusercontent.com/xbunax/blogImg/main/202404051310231.png)

