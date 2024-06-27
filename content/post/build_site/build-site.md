---
title: "Build Site"
description: 
date: 2024-06-27T10:13:40+08:00
image: https://raw.githubusercontent.com/xbunax/blogImg/main/202406271246388.png 
math: 
license: 
hidden: false
comments: true
draft: false
---



## Short Brief

我们常常需要展示一些个人作品，简历或者单纯分享，这时候你可以发b站视频，知乎文章，但是更优雅的做法当然是利用GitHub Page做一个自己的网站啦，拥有更强的自定义功能，不需要通过平台的审核，并且如果不需要个人域名的话是完全免费的。

## Prepare

我们简单介绍一下实现的原理，每个GitHub账号都可以创建一个`Username.github.io`这个仓库，可以托管网站并且渲染`HTML`文件。

所以我们需要一个GitHub账号，如果需要域名访问的话，还需要购买域名。同时因为`github.io`是渲染的`HTML`，但是写网页用纯html对于我们来说还是太麻烦了，所以我们一般是利用`markdown`写文章然后编译成`HTML`利用git提交到`github.io`仓库，当然这些都有现成的转换工具，笔者习惯用`hugo`，之后会介绍如何部署。

  > 需要的软件:
  > + git以及GitHub账号 
  > + hugo
  > + `brew install hugo git`
  > + 需要一些命令行操作`cd ls`以及git的基础操作

## Deploy

首先我们在GitHub上创建一个名为`Username.github.io`的public仓库，其中`Username`是GitHub账号的用户名，并添加`README`文件，同时我们再创建一个repo，用来存放整个网站的数据。然后将这个仓库git clone到本地(git clone repo-url)，接着`cd`到仓库的文件夹，利用`hugo`创建站点，在终端中输入`hugo new site /current-repo-path && hugo`，`hugo`会在当前文件夹生成一些文件。

```
current-repo-path
├── archetypes 存放用 hugo 命令新建的 Markdown 文件应用的格式模板
├── assets 
├── content 存放 hugo 创建的markdown文件
├── data
├── hugo.toml 
├── i18n
├── layouts
├── static 存放静态文件或者图片
├── public 存放 hugo 生成的静态网站的html文件
└── themes 设置 hugo 的主题
```

我们就是将生成的public文件夹的文件push到`Username.github.io`这个仓库，所以我们可以将GitHub Page的仓库clone到public文件夹`git clone https://github.com/Username.github.io public`，或者到public文件夹下面利用`git init`命令创建一个本地git仓库，再利用`git set remote url`与GitHub上的`Usename.github.io`仓库链接。
  > 同时要把hugo的默认配置文件即`config/_default/config.toml`中的`baseurl`设置成`github.io`的仓库链接，如果有域名则设置成域名。

## Theme 

我们网页肯定希望有一些美化，可以去[hugo官方主题](https://themes.gohugo.io/)去找对应的主题，并且对应主题有安装的`README`。笔者本人选用的是[hugo stack](https://themes.gohugo.io/themes/hugo-theme-stack/)主题，作者同时也提供了方便部署的仓库，只需要将`https://github.com/CaiJimmy/hugo-theme-stack-starter`这个仓库clone到本地就可以了。
![hugo stack](https://raw.githubusercontent.com/xbunax/blogImg/main/202406271236171.png)

## Release

接着我们就要发布第一篇文章了，创建一篇新文章的方法即`hugo new first.md`，`hugo`会在`content`目录下创建文章，你可以为这篇文章单独创建一个文件夹放置到`content/post/`文件夹下。新创建的`markdown`文件头有meta数据以本篇文章为例
```
---
title: "Build Site"
description: 
date: 2024-06-27T10:13:40+08:00
image: #设置文章封面
math: #是否开启数学公式渲染
license: #开源证书
hidden: false
comments: true #是否开启评论区这个要单独部署评论区的服务属于进阶用法比较复杂本文章暂不涉及
draft: false #是否是草稿
---
```
同时你还可以设置文章的分类和标签，如果想要进一步设置可以看作者写的[文档](https://stack.jimmycai.com/guide/getting-started)。以下是笔者本人设置之后的页面样式。
![my blog](https://raw.githubusercontent.com/xbunax/blogImg/main/202406271246388.png)


## Summarize

使用静态网站展示个人作品以及分享一些文章是非常方便的事情，只需要让对方访问个人网站即可，并且不需要像动态网站那样需要服务器费用以及维护的精力。笔者本人曾利用`wordpress`部署过动态网站，但是发现文章排版相当麻烦而且运营维护还有云服务开销并不划算，所以最后还是放弃了原来的方案，利用GitHub Page部署个人网站。
