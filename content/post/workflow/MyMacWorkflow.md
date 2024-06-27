---
title: "MyMacWorkflow"
description: 
date: 2024-03-05T17:13:34+08:00
image: https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/cover.png
math: 
license: 
categories: [
"workflow",
"MacOS",
"Unix-like"
]
hidden: false
comments: true
draft: false
toc: true
---
<!-- ![cover](https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/cover.png) -->
<!-- *spotify tui* -->

# My Mac Workflow

作为一个六年的Mac用户，从2018款macbook pro到M2芯片的macbook air，积累了很多Mac的使用心得与好用的软件。在此分享一下我在Mac上的workflow。

> - Tips：本人专业背景为理论物理，主要科研工作偏向使用`Unix-like`系统，所以不会涉及windows(但是可以使用`wsl2`)。
> - 推荐安装`homebrew`作为MacOS上的包管理器。 


<!-- ## Reserch  -->

### Zotero

- 作为科研狗第一重要的事当然是看文献了，那么一个好的文献管理器至关重要，虽然学校提供了正版的EndNote但是相比而言更喜欢免费的Zotero，并且可以安装第三方插件，例如我装了preview插件可以预览文献内容。
并且我主要使用latex为论文排版，Zotero可以快速导出bibtex文件方便在论文中引用文献。
- 同时Zotero可以利用官方提供的网盘进行多平台同步，但是免费容量只有5G，一般来说够用但是为了长远考虑，我使用微软学生认证提供的2T OneDrive挂载到koofr实现webDAV，这样就能使用白嫖到的2T空间做同步备份了。

![zotero](https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/zotero.png)


### Material Project

作为广大炼丹烧炉子研究工作者，在科研中肯定遇到要查询材料参数的情况，[MaterialProject](https://next-gen.materialsproject.org/)，这个网站作为材料领域做高通量计算方向搭建的，囊括了大量的材料参数，并且作为开源项目的一部分，此网站还提供了`python`的`package(pymatgen)`方便调用网站的api，可以获取材料的晶格结构等并且给出相关的文献。

<!-- ![material](https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/material.png) -->

![material](https://raw.githubusercontent.com/xbunax/blogImg/main/202403091438804.png)
### Pngpaste 

我的论文写作工具主要是`neovim`+`latex`，但是由于饱受`latex`上古语法困扰最近也在尝试`typst`并且得益于`neovim`活跃的社区，`typst`的`lsp`还有双向链接工具已经完全可用了。

不管是`latex`还是`typst`写作时一直有一个痛点那就是插入图片，往往我会将图片截图存在剪贴板中，但是在用`neovim`写论文时，经常要切出去保存图片非常影响效率。这时候我们就可以用`pngpaste`这个CLI工具，可以在命令行环境下读取剪贴板图片保存为`png`格式，这样在`neovim`中用`toggleterm`插件写一个`autocmd`自动保存剪贴板图片，大大提升了效率。


### Window Manager

由于苹果的封闭，Mac上的窗口管理器选择并不是很多，`yabai`虽然可以实现平铺窗口管理器的大部分功能，但是需要关闭SIP，无法在Mac上使用iPad和iPhone应用也无法使用Touch ID支付。博主本人尝试过后发现bug相对较多，而且`yabai`的主要贡献者只有作者一人，`yabai`调用的api非常底层，每次苹果更新系统过都要等待作者适配，就体验来说并不是很好。

现在博主主力的window Manager是`amethyst`。相比于`yabai`的优势在于不用关闭SIP所以相对来说受系统版本变化影响较小，而且`amethyst`配置相对简单，基本等于开箱即用，设置好快捷键键位就可以用了，不需要像`yabai`设置好`yabairc`还需要利用`skhd`再去映射快捷键，虽然可以直接抄大佬的配置，但是需要踩的坑还是相对多一点。

但是不需要关闭SIP，就意味着相较于`yabai`，`amethyst`相对而言还是缺少了类似于创建销毁窗口，设置windows animation全局窗口透明度这些功能。但是`amethyst`作为平铺窗口管理还是合格了，快速移动窗口，一键更改布局，单独设置float窗口.
