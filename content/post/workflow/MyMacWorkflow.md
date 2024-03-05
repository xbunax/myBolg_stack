---
title: "MyMacWorkflow"
description: 
date: 2024-03-05T17:13:34+08:00
image: https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/cover.png
math: 
license: 
hidden: false
comments: true
draft: false
toc: true
---
<!-- ![cover](https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/cover.png) -->
<!-- *spotify tui* -->

# My Mac Workflow

作为一个六年的Mac用户，从2018款macbook pro到M2芯片的macbook air，积累了很多Mac的使用心得与好用的软件。在此分享一下我在Mac上的workflow。

- Tips：本人专业背景为理论物理，主要科研工作偏向使用`Unix-like`系统，所以不会涉及windows(但是可以使用`wsl2`)。


## Reserch 

### Zotero

- 作为科研狗第一重要的事当然是看文献了，那么一个好的文献管理器至关重要，虽然学校提供了正版的EndNote但是相比而言更喜欢免费的Zotero，并且可以安装第三方插件，例如我装了preview插件可以预览文献内容。
并且我主要使用latex为论文排版，zotero可以快速导出bibtex文件方便在论文中引用文献。
- 同时zotero可以利用官方提供的网盘进行多平台同步，但是免费容量只有5G，一般来说够用但是为了长远考虑，我使用微软学生认证提供的2T OneDrive挂载到koofr实现webDAV，这样就能使用白嫖到的2T空间做同步备份了。

![zotero](https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/zotero.png)


### Material Project

作为广大炼丹烧炉子研究工作者，在科研中肯定遇到要查询材料参数的情况，[MaterialProject](https://next-gen.materialsproject.org/)，这个网站作为材料领域做高通量计算方向搭建的，囊括了大量的材料参数，并且作为开源项目的一部分，此网站还提供了`python`的`package(pymatgen)`方便调用网站的api，可以获取材料的晶格结构等并且给出相关的文献。

![material](https://raw.githubusercontent.com/xbunax/blogImg/main/workflow/material.png)



