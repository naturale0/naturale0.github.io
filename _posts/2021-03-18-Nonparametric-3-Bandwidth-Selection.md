---
layout: post
title: "3. Bandwidth Selection"
date:   2021-03-18 16:55:00 +0900
author: "Sihyung Park"
categories: [nonparametric]
---



Recall that the optimal bandwidth $h_\text{opt}$ derived from MISE was given as the following:


$$
h_\text{opt} = \left( \frac{\int K^2}{\mu_2(K) \int p''(x)^2 dx} \right)^{1/5} n^{-1/5}.
$$


However since $p$ is unknown, we cannot use this directly. Rather, we need an appropriate estimate of $\int p''(x) dx$ to do get a usable bandwidth.



- TOC
{:toc}
<br> 

## Normal reference

If we assume that $p=\phi_\sigma,$ that is the true density $p$ is actually a density of normal distribution with mean zero and variance $\sigma^2,$ then using the properties of gaussian derivatives


$$
\phi'(x) = -x\phi(x), \\
\phi''(x) = (x^2-1)\phi(x),
$$


we get 


$$
\begin{aligned}
\int (p'')^2
 &= \int \left( \frac{1}{\sigma^3}\phi''(x/\sigma) \right)^2 dx \\
 &= \frac{1}{\sigma^5} \int \phi''(y)^2 dy \\
 &= \frac{1}{\sigma^5} \frac{1}{\sqrt{4\pi}} \int (y^4 - 2y^2 + 1) \phi_\frac{1}{\sqrt{2}}(y) dy \\
 &= \frac{1}{\sigma^5} \frac{1}{2\sqrt{\pi}} \int (z^4/4 - z^2 + 1) \phi(z) dz \\
 &= \frac{1}{\sigma^5} \frac{1}{2\sqrt{\pi}} \left( \frac{1}{4} K \cancel{- 1} \cancel{+ 1} \right) \\
 &= \frac{1}{\sigma^5} \frac{1}{2\sqrt{\pi}} \frac{3}{4} \\
 &= \frac{3}{8\sqrt{\pi}}\frac{1}{\sigma^5}.
\end{aligned}
$$


By plugging this in, we get our **normal reference bandwidth**


$$
\hat h_\text{NS} = \left( \frac{8\sqrt{\pi}}{3} \frac{\int K^2}{\mu_2(K)^2} \right)^{1/5}n^{-1/5} \cdot\hat\sigma^5,
$$


where $\hat\sigma$ can be estimated in two different ways: (1) use sample standard deviation, or (2) use interquartile range (IQR). Motivation behind IQR-based $\hat\sigma$ estimation is that


$$
\begin{aligned}
\hat F^{-1}(3/4) - \hat F^{-1}(1/4)
 &\approx \hat \Phi_\sigma^{-1}(3/4) - \hat \Phi_\sigma^{-1}(1/4) \\
 &= \sigma \left(\hat \Phi^{-1}(3/4) - \hat \Phi^{-1}(1/4)\right)
\end{aligned}
$$


so we estimate $\sigma$ with


$$
\hat\sigma = \frac{\hat F^{-1}(3/4) - \hat F^{-1}(1/4)}{\hat \Phi^{-1}(3/4) - \hat \Phi^{-1}(1/4)}.
$$


<br>

## Oversmoothing

It is known that


$$
\sup_{p \in \mathcal{F}_\sigma} \frac{\int K^2}{\mu_2(K)^2 \int (p'')^2} = \frac{243}{35} \frac{\int K^2}{\mu_2(K)^2} \sigma,
$$


where $\mathcal{F}_\sigma$ is the collection of densities with variance $\sigma^2.$ ($\int u^2p(u)du - (\int up(u)du)^2 = \sigma^2.$) We can simply use this upper bound as our bandwidth, with $\hat\sigma$ estimated as the above.


$$
\hat h_{OS} = \frac{243}{35} \frac{\int K^2}{\mu_2(K)^2} \hat\sigma.
$$


We call this the **oversmoothed bandwidth selector**, since it will certainly be larger than $h_\text{opt}$ if the variance assumption is true, and the larger the bandwidth, the smoother the density estimate we get.

<br>

## Least squares cross-validation

Recall that $h_\text{opt}$ minimizes AMISE, and hopefully MISE.


$$
\begin{aligned}
\text{MISE}(\hat p)
 &= E\int \left( \hat p(x) - p(x) \right)^2 dx \\
 &= E\int \hat p(x)^2 dx - 2E\int \hat p(x)p(x)dx + E\int p(x)^2dx.
\end{aligned}
$$


Observe that the last term is independent to $h$ so we only focus on the first two terms.


$$
\begin{aligned}
\text{MISE}(\hat p) - E\int p(x)^2dx
 &= E\int \hat p(x)^2 dx - 2E\int \hat p(x)p(x)dx \\
 &= E\left[ \int \hat p(x)^2 dx - \frac{2}{n} \sum_{i=1}^n \hat p_{-i}(X_i) \right],
\end{aligned}
$$


where 


$$
\hat p_{-i}(X_i) := \frac{1}{n-1} \sum_{j\ne i} K_h(x-X_j).
$$


<div class="proof"><br>
$$
\begin{aligned}
E\hat p_{-i}(X_i)
 &= E\left[ E(\hat p_{-i}(X_i)|X_i) \right] \\
 &= E\left[ \frac{1}{\cancel{n-1}}\cancel{(n-1)} \int K_h(X_i-X_j)p(X_i)dX_i \right] \\
 &= E\left[ K_h * p(X_i) \right] \\
 &= E\left[ E(\hat p(X_i) | X_i) \right] \\
 &= E\int \hat p(x)p(x) dx.
\end{aligned}
$$



</div> 



The **least squares cross-validation selector (LSCV)** chooses $\hat h_\text{LSCV}$ by obtaining a minimizer of 


$$
\begin{aligned}
\text{LSCV(h)}
 ~=& \int \hat p(x)^2 dx - \frac{2}{n} \sum_{i=1}^n \hat p_{-i}(X_i) \\
 =& \frac{1}{n^2} \sum_i\sum_j K_h * K_h(X_i-X_j) \\
  & - \frac{2}{n(n-1)} \sum_{i} \sum_{j\ne i} K_h(X_i - X_j).
\end{aligned}
$$


which is the integrand of MISE. The second equality holds if $K$ is symmetric.



<div class="proof"><br>
$$
\begin{aligned}
\int \hat p^2
 &= \frac{1}{n^2} \sum_{i=1}^n \sum_{j=1}^n \int K_h(x-X_i)K_h(x-X_j) dx \\
 &= \frac{1}{n^2} \sum_{i=1}^n \sum_{j=1}^n \int K_h(w + X_j - X_i) K_h(w) dw \\
 &= \frac{1}{n^2} \sum_{i=1}^n \sum_{j=1}^n \int K_h(X_i - X_j - w) K_h(w) dw \\
 &= \frac{1}{n^2} \sum_{i=1}^n \sum_{j=1}^n K_h * K_h (X_i-X_j).
\end{aligned}
$$

In the second equality, $x-X_j$ was substituted to $w,$ and in the third equality, symmetry of $K$ was used.

</div> 



We define LSCV bandwidth selector as


$$
\hat h_\text{LSCV} = \argmin_{h>0} \text{LSCV}(h).
$$


<br>

## $k$-fold LSCV

Although the LSCV gives better bandwidth than normal referencing or oversmoothing, it is computationally heavy since it requires $n^2$ order of operations. To relieve the computational stress, $k$-fold LSCV was devised.

Instead of using "leave-one-out" density estimate $\hat p_{-i},$ $k$-fold LSCV uses "leave-many-out" estimate $\hat p_{A_i}.$ Formal definition is as follows: let $A_1,\cdots,A_k$ be a partition of the index set $\\{1,2,\cdots,n\\},$ and define


$$
\hat p_{-A_i} := \left( \sum_{i=1}^n \mathbf{1}(i \notin A_i) \right)^{-1} \sum_{i \in A_i} K_h(x-X_i).
$$


$k$-fold LSCV is defined accordingly.


$$
\text{LSCV}^\text{$k$-fold}(h) = \int \hat p(x)^2 dx - \frac{2}{k} \sum_{l=1}^k \left( \left(\sum_{i=1}^n \mathbf{1}(i \in A_l)\right )^{-1} \sum_{i \in A_l} \hat p_{-A_l}(X_i) \right).
$$




Notice that now linear order ($\sim N$) of computation is enough since $k$ is prespecified (mostly, $k=5$ for $10$). $E \left[ \text{LSCV}^\text{$k$-fold}(h) \right]$ is the same as in standard LSCV. Finally, $k$-fold LSCV selector is


$$
\hat h_\text{LSCV}^\text{$k$-fold} = \argmin_{h>0} \text{LSCV}^\text{$k$-fold}(h).
$$


<br>

## Other selectors

### Biased cross-validation

Biased cross-validation (BCV) is a hybrid of normal reference-type plug in selector and LSCV-type cross validation selector. Recall that the bias expansion gives


$$
\text{AMISE} = \frac{1}{4}h^4 \mu_2(K)^2 \int (p'')^2 + \frac{1}{nh} \int K^2
$$


The idea of BCV is to replace $\int (p'')^2$ by 


$$
\int (\hat p'')^2 = \frac{1}{n^2} \sum_{i=1}^n \sum_{j=1}^n K_h'' * K_h'' (X_i-X_j)
$$


to get


$$
\text{BCV}(h) = \frac{1}{4}h^4 \mu_2(K)^2 \int (\hat p'')^2 + \frac{1}{nh} \int K^2.
$$




(The proof is the same as in LSCV.) $\hat h_\text{BCV}$ is defined as a minimizer of BCV.

<br>

### Selectors that converges faster

One can show that LSCV and BCV selector both converge unbearably slowly to the true $h_\text{opt}$:


$$
\left( \frac{\hat h_\text{LSCV}}{h_\text{opt}} - 1 \right) n^{1/10} \overset{\text{d}}{\to} \mathcal{N}(0, \sigma^2_\text{LSCV}).
$$


That is the order of $n^{1/10}$: to make $n^{1/10}$ grow from 0 to 2, a thousand of samples is required! As remedies of this problem, **solve-the-equation rule** ($\sim n^{4/13},$ later improved to $\sim n^{5/14}$) and **smoothed CV** ($\sim n^{1/2}$) selectors are proposed.





<br>

***References***

* **Nonparametric Function Estimation (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Byeong U. Park).
* [**Nonparametric Statistics**](https://bookdown.org/egarpor/NP-UC3M/), by Eduardo García Portugués.

