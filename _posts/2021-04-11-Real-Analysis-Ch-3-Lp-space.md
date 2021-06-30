---
layout: post
title: "3. $L^p$ Space"
date:   2021-04-11 14:01:00 +0900
author: "Sihyung Park"
categories: [real analysis, Real and Complex Analysis]
---



As we defined the Lebesgue integral and proved the basic properties, it is time to study the space of functions with finite integrals.

## Inequalities

<div class="theorem" text="Jensen">

$(X, \mathfrak{M}, \mu)$: a measure space where $\mu(X) = 1.$<br>

$\varphi: \mathbb{R} \to \mathbb{R}$ is convex on $(a,b).$<br>

$f: X \to (a,b).$ Then,
$$
\varphi\left(\int f d\mu\right) \le \int \varphi \circ f d\mu.
$$
</div> <br>



<div class="theorem" text="Hölder">

$f, g \ge 0,$ $\frac{1}{p}+\frac{1}{q}=1,$ $p,q> 1,$ then
$$
\int fg d\mu \le \left(\int f^p d\mu\right)^{1/p} \left(\int g^q d\mu\right)^{1/q}.
$$
</div> <br>



<div class="theorem" text="the element of the smallest norm">
Let $E \sub H$ be a non-empty, closed, convex set. Then there uniquely exists $x \in E$ that satisfies
$$
\|x\| = \inf_{y \in E} \|y\|.
$$
</div>


$f,g \ge 0,$ $p \ge 1,$ then
$$
\int (f+g)^p d\mu \le \int f^p d\mu + \int g^p d\mu.
$$
</div> <br>

## $L^p$ space

### $1\le p<\infty$

<div class="theorem" text="">

$L^p(\mu)$ is complete in $\|\cdot\|_p.$

</div> 

<div class="proof"><br>
Given a Cauchy sequence $(f_n) \in L^p(\mu)$ and $\epsilon>0.$ There exists a subsequence $(f_{n_k})$ such that 
$$
\|f_{n_{k+1}} - f_{n_{k}}\|_p < \frac{1}{2^k},~ \forall k.
$$
And let
$$
g_n = \sum_{k=1}^n |f_{n_{k+1}} - f_{n_{k}}|, \\
g = \sum_{k=1}^\infty |f_{n_{k+1}} - f_{n_{k}}|.
$$
Then clearly $g_n \uparrow g$ and $g_n \ge 0.$ By monotone convergence,
$$
\|g_n\|_p \uparrow \|g\|_p \le 1 < \infty.
$$
This implies $g < \infty$ almost everywhere. Now, note that
$$
f_{n_{k}} = f_{n_1} + \sum_{i=1}^{k-1}\left( f_{n_{i+1}} - f_{n_{i}} \right)
$$
and define
$$
f = f_{n_1} + \sum_{i=1}^{\infty}\left( f_{n_{i+1}} - f_{n_{i}} \right)
$$
Then
$$
\begin{aligned}
|f| \le |f_{n_1}| + g < \infty ~\text{ a.e.}   && \text{($|f_{n_1}|, g < \infty$ almost everywhere)}
\end{aligned}
$$
Thus $f_{n_k} \to f$ almost everywhere as $k \to \infty.$ Our claim is that $f_n \overset{L^p}{\to} f.$<br>

For $\epsilon > 0,$ there exists $N\in\mathbb{N}$ such that $\|f_n - f_{n_k}\|_p < \epsilon$ for all $n, k \ge N.$
$$
\begin{aligned}
\int |f_n - f|^p d\mu
 &= \int \liminf_k |f_n - f_{n_k}|^p d\mu \\
 &\le \liminf_k \int |f_n - f_{n_k}|^p d\mu \\
 &< \epsilon^p  ~~\text{for $n \ge N$}.
\end{aligned}
$$

$$
\therefore \|f_n - f\|_p < \epsilon,~ \forall n \ge N.
$$

</div> <br>



### $p=\infty$

<div class="theorem" text="">
$L^\infty(\mu)$ is complete with respect to $\|\cdot\|_\infty.$

</div> 

<div class="proof"><br>
uniformly cauchy
</div> <br>



## Continuous approximation

### $L^p(\mu)$ and $C_c(X)$



* $S$ ~ $L^p$
* Lusin's theorem
* $C_c(X)$ ~ $L^p$



### $C_0(X)$ and $C_c(X)$

* $C_c$ is dense in $C_0$
* $C_0$ is complete





<br>

***References***

* Rudin. 1986. **Real and Complex Analysis**. 3rd edition. McGraw-Hill.
* **Real Analysis (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Insuk Seo).