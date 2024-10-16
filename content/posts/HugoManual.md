---
title: HugoManual
date: 2024-10-14
author: "111111111"
math: true
bookHidden: false
math: true
bookSearchExclude: true
---
hugo使用手册
  <!--more-->
## Search

搜索 coconut
谭浩

---

## RealReference

## RelativeReference

[Reference]({{< ref "_index" >}})
```
[Reference]({{< ref "_index" >}})
```
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
