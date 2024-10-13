---
title: "HugoManual"
date: 2024-10-13T15:49:15+08:00
author: "111111111"
bookSearchExclude: true
bookHidden: true
---
  <!--more-->

- [Buttons]({{< relref "/docs/shortcodes/buttons" >}})
- [Columns]({{< relref "/docs/shortcodes/columns" >}})
- [Expand]({{< relref "/docs/shortcodes/expand" >}})
- [Hints]({{< relref "/docs/shortcodes/hints" >}})
- [KaTeX]({{< relref "/docs/shortcodes/katex" >}})
- [Mermaid]({{< relref "/docs/shortcodes/mermaid" >}})
- [Tabs]({{< relref "/docs/shortcodes/tabs" >}})

## RealReference
[Columns]({{< relref "/docs/shortcodes/columns" >}})
```
[文章<<Columns>>的引用测试]({{< relref "/docs/shortcodes/columns" >}})
```
---
## RelativeReference
[Reference]({{< ref "_index" >}})
```
[Reference]({{< ref "_index" >}})
```
---

## Button

{{< button relref="/" >}}Get Home{{< /button >}}
{{< button href="https://github.com/alex-shpak/hugo-book" >}}
Contribute{{< /button >}}{{< button relref="/" >}}Get Home{{< /button >}}

---
## Columns

{{< columns >}}
## Left Content
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
protulit, sed sed aere valvis inhaesuro Pallas animam: qui _quid_, ignes.
Miseratus fonte Ditis conubia.

<--->

## Mid Content
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter!

<--->

## Right Content
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
protulit, sed sed aere valvis inhaesuro Pallas animam: qui _quid_, ignes.
Miseratus fonte Ditis conubia.
{{< /columns >}}

## Block
### Block1
```
qweqweeqweqweqwe
```
### Block2
    cpp
    qweqweqwe
    qwe
    qwe
    qwe

## 