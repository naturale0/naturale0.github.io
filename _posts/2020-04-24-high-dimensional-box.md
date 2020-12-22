---
layout: post
title:  "High-dimensional box"
date:   2020-04-24 18:37:10 +0900
author: "Sihyung Park"
categories: probability
---

<div class="example" text='High-dimensional box'>
Consider an $n$-dimensional box $[-1, 1]^n$. Suppose we randomly pick an element from this box. i.e. $\mathbf{X_n}=(X_1, \cdots, X_n)$, where $X_1, \cdots, X_n \stackrel{iid}{\sim} \mathcal{U}(-1,1)$. Then as $n \to \infty$, $P(\sqrt{\frac{n}{3}(1-\epsilon)}< \|\mathbf{X_n}\|_2 < \sqrt{\frac{n}{3}(1+\epsilon)}) \to 1$, $\forall{0<\epsilon<1}$.
</div>



This implies that the probability of observing the element at the surface of the box becomes 1 as the dimension increases. This is one of the properties of high-dimensional problems which makes them challenging.
