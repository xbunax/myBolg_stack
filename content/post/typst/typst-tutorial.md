---
title: "Typst Tutorial"
description: 
date: 2024-06-08T14:01:20+08:00
image: https://raw.githubusercontent.com/xbunax/blogImg/main/202406091609355.png
math: 
license: 
categories: [
"workflow",
"Typst",
]
hidden: false
comments: true
draft: false
---
# Typst tutorial

## Typst介绍

`Typst`是新的基于标记的科学排版语言其目标是作为`LaTex`的替代，因为`Typst`底层采用`Rust`编写,所以在编译效率上比`LaTex`高了非常多，基本上可以做到实时预览并且语法相当友好。

`LaTex`由于其诞生于上世纪80s时间过早，并且经过几十年的发展技术包袱过重。笔者本科用`LaTex`排版论文经常苦于语法晦涩，一旦环境嵌套过深代码几乎失去可读性，并且一旦插入图片过多以及加入`bibtex`那么编译时间会极大拉长，只能将`LaTex`分章节编译。

如果你也苦于`LaTex`的以上问题，那么`Typst`绝对值得尝试，`Typst`于2023年开源开始release，`Typst`社区非常活跃，笔者在2023年下半年开始使用，半年时间`nvim`和`vscode`的全套工具链就已经可用[`tinymist`](https://github.com/Myriad-Dreamin/tinymist)，[`typstyle`](https://github.com/Enter-tainer/typstyle/)，[`typst-preview`](https://github.com/chomosuke/typst-preview.nvim)。

## Typst 语法介绍

`Typst`语法上相对`LaTex`简洁很多，不需要像`LaTex`那样进行`\bengin` `\end`环境嵌套。

### Typst添加标题
```typst
= Introduction ##一级标题

== subsection ##二级标题

=== subsubsection ##三级标题
```

### Typst有序和无序列表

```typst
+ The climate
  - Temperature
  - Precipitation
+ The topography
+ The geology
```


<img src="https://raw.githubusercontent.com/xbunax/blogImg/main/202406091522850.png" width="50%"/>


### Typst插入图表与引用

```typst
Glaciers as the one shown in
@glaciers will cease to exist if
we don't take action soon!

#figure(
  image("glacier.jpg", width: 70%),
  caption: [
    _Glaciers_ form an important part
    of the earth's climate system.
  ],
) <glaciers>
```

<img src="https://raw.githubusercontent.com/xbunax/blogImg/main/202406091524014.png" width="50%"/>

### Typst数学公式

`Typst`数学公式语法并没有学习`LaTex`而是添加了一些OOP的语法，并且简化了特殊符号的输入增强了公式的可读性。

```typst
$Q = rho A v + C$  ##typst中如果是内联公式就不需要在`$`后空格，反之则是单独一行
```
上式就相当于`LaTex`中的$Q=\rho A v + C$，如果是复杂一点的公式则可能会更清晰一点比较两者之间的区别。

```
$ 7.32 beta +sum_(i=0)^nabla (Q_i (a_i - epsilon)) / 2 $
```

```LaTex
7.32 \beta + \sum_{i=0}^{\nabla} \frac{Q_i (a_i - epsilon)}{2}
```
$$
7.32 \beta + \sum_{i=0}^{\nabla} \frac{Q_i (a_i - \epsilon)}{2}
$$

如果是一些特殊符号`Typst`则添加了一些OOP的元素比如
```typst
$ a arrow.squiggly b $
```

<img src="https://raw.githubusercontent.com/xbunax/blogImg/main/202406091536833.png" width="50%"/>

### LaTex用户快速上手对照表

`typst`官方也贴心的为`LaTex`用户提供了快速的[语法对照表](https://typst.app/docs/guides/guide-for-latex-users/)可以查看

| Element            | LaTeX                        | Typst                         | See      |
|--------------------|------------------------------|-------------------------------|----------|
| Strong emphasis    | `\textbf{strong}`            | `*strong*`                    | [strong](https://typst.app/docs/reference/model/strong/)  |
| Emphasis           | `\emph{emphasis}`            | `_emphasis_`                  | [emph](https://typst.app/docs/reference/model/emph/)  |
| Monospace / code   | `\texttt{print(1)}`          | `` `print(1)` ``              | [raw](https://typst.app/docs/reference/text/raw/)  |
| Link               | `\url{https://typst.app}`    | `https://typst.app/`          | [link](https://typst.app/docs/reference/model/link/)  |
| Label              | `\label{intro}`              | `<intro>`                     | [label](https://typst.app/docs/reference/foundations/label/)  |
| Reference          | `\ref{intro}`                | `@intro`                      | [ref](https://typst.app/docs/reference/model/ref/)  |
| Citation           | `\cite{humphrey97}`          | `@humphrey97`                 | [cite](https://typst.app/docs/reference/model/cite/)  |
| Bullet list        | `itemize` environment        | `- List`                      | [list](https://typst.app/docs/reference/model/list/)  |
| Numbered list      | `enumerate` environment      | `+ List`                      | [enum](https://typst.app/docs/reference/model/enum/)  |
| Term list          | `description` environment    | `/ Term: List`                | [terms](https://typst.app/docs/reference/model/terms/)  |
| Figure             | `figure` environment         | `figure` function             | [figure](https://typst.app/docs/reference/model/figure/)  |
| Table              | `table` environment          | `table` function              | [table](https://typst.app/docs/reference/model/table/)  |
| Equation           | `$x$, align / equation environments` | `$x$, `$ x = y $` | [equation](https://typst.app/docs/reference/math/equation/)  |


## Typst制作Slides

`Typst`目前制作`Slides`的体验比`LaTex`制作`Beamer`好了很多，我们以[`tongji-slides-typst`](https://github.com/TJ-CSCCG/tongji-slides-typst)为例简单展示一下`Typst`的`Slides`。

```
#matrix-slide[
== EXAMPLE
#align(
  top + left, [== DMI效应产生原因
  #v(1em)
  - DMI是由于反演对称性破缺和`Spin-Orbit Couple`(SOC)引起的反对称交换作用

  - 在具有非对称晶体结构的材料中，由于原子排列的不均匀性，电子在原子间运动时会经历不均匀的电场。这个不均匀的电场改变了自旋-轨道耦合的性质，导致电子的自旋倾向于以特定的方式与其轨道运动相耦合。这种耦合产生了一个优先的方向，使得磁矩倾向于非对易地排列。

  #figure(image("pic/DMI_1.png", height: 40%), caption: [
    Dzyaloshinskii–Moriya interaction
  ])

  ],
)

][
#v(1em)
#align(
  top + left, [
  - DMI效应最早发现于$alpha-"Fe"_2"O"_3$反铁磁材料中，实验上发现了弱铁磁性。

  - Dzyaloshinskii给出了唯象的解释$H_("DM")=D dot [S_i times S_j]$，即DMI相互作用使相邻磁矩趋于垂直。

  - Moriya结合超交换理论提出这种效应可以看作是磁绝缘体中SOC以及对称性破缺所引起的附加项。

  - 在相互交换作用和DMI的共同作用下，磁矩会趋于形成一定夹角，因此会形成`SKyrmions`结构。

  #figure(image("pic/SKyrmion.png", height: 39%), caption: [`SKyrmions`结构])

  ],
)
]
```

<img src="https://raw.githubusercontent.com/xbunax/blogImg/main/202405181220107.png"/>

这里是通过模板封装好了`#matrix-slide`只需要通过`import`调用调用即可。如果是设置封面则只需要调用封装好的函数修改其暴露的接口即可。

```
#title-slide(
  authors: ("李狗蛋", "蛋狗李"), title: "Tongji slides typst", subtitle: "Template", date: "Date", institution-name: "Tongji University",
)
```

<img src="https://raw.githubusercontent.com/xbunax/blogImg/main/202405181220130.png"/>

`Typst`的制作`Slides`的体验与代码可读性比`LaTex`的环境嵌套要好很多。如果要使用这里推荐[touying](https://github.com/touying-typ/touying)这是国人编写的一个`Slides`包体验相对较好。

## Typst当前发展

`Typst`目前已经开放了[`Universe`](https://typst.app/universe/)提供了各种模板可选，在`Typst`社区活跃度较高国人也相对较多，已经有很多优秀的`package`是国人编写的。国内高校也有了一些优秀的开源模板项目，比如同济的[`tongji-undergrad-thesis-typst`](https://github.com/TJ-CSCCG/tongji-undergrad-thesis-typst)。

`package`这里推荐[`miTex`](https://typst.app/universe/package/mitex)，如果你实在不习惯用`Typst`的公式语法第三方也提供了使用`LaTex`的公式接口。
同时`Typst`也支持[`cetz`](https://typst.app/universe/package/cetz/)绘制矢量图。

总之`Typst`社区还在快速发展中，作为`LaTex`的老用户笔者也同时希望在`Typst`的竞争下能够更好。
