---
title: HugoManual
date: 2024-10-14
author: "111111111"
bookSearchExclude: true
bookHidden: false
math: true
---
hugo使用手册
  <!--more-->
## RealReference
[Games101]({{< relref "/posts/2024-06-23 GAMES101.md" >}})

```
[Games101]({{< relref "/posts/2024-06-23 GAMES101.md" >}})
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

---

## Math Suport  
### katex  latex   

https://katex.org/docs/browser.html  
blog：  
https://mertbakir.gitlab.io/hugo/math-typesetting-in-hugo/  
https://edwinkofler.com/posts/render-latex-with-katex-in-hugo-blog/  
themes\hugo-book\layouts\partials\docs\html-head.html  
themes\hugo-book\layouts\partials\docs\katex.html
### use "///"
use "///" because"//" is not work for line break.


---

## Math function order

$$
I(\mathbf{p}, \mathbf{d}) = E(\mathbf{p}, \mathbf{d}) + \int_{\Omega} f_r(\mathbf{p}, \mathbf{d}, \mathbf{d'}) L(\mathbf{p}, \mathbf{d'}) \cos(\theta') \, d\mathbf{d'}
$$

$$
\begin{equation}
f(x) = \int_{-\infty}^\infty\hat f(\xi)\,e^{2 \pi i \xi x}\,d\xi
\end{equation}
$$


	 // first equation whitout number
	// second one with number cause use this 
	```````````````````````````````````````

	\begin{equation}
	math function
	\end{equation}

	````````````````````````````````````````

---

