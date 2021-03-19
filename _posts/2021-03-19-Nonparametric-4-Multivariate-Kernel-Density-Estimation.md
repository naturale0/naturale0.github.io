---
layout: post
title: "[Nonparametric] 4. Multivariate Kernel Density Estimation"
date:   2021-03-19 10:41:00 +0900
author: "Sihyung Park"
categories: [non-parametric]
---



Until now, I only covered univariate cases. From now on, our focus is on multivariate cases where samples $X_1,\cdots,X_n\in\mathbb{R}^d$ are independently drawn from the density $p:\mathbb{R}^d\to[0,\infty)$ with respect to the Lebesgue measure.



- TOC
{:toc}
<br> 

## Kernel and bandwidth settings

### Kernel function

We need a $d$-variate kernel function $\kappa$ for this. There are several possible ways to define it.

1. **Product kernel**: 

    $$
    \kappa(x) := \prod_{j=1}^d K(x_j),
    $$

    where $K:\mathbb{R}\to\mathbb{R}$ is a univariate function with $\int K = 1.$

2. **Radially symmetric kernel**: 


    $$
    \kappa(x) := K(x^\intercal x),
    $$

    where $K:\mathbb{R}\to\mathbb{R}$ is a univariate function with $\int K(x^\intercal x)dx = 1.$



We will focus on the simple case of using product kernel.

<br>

### Bandwidth

Now the bandwidth is also multivariate. Three choices of bandwidth are available.

1. **Scalar bandwidth**:

    Use the same $h\in\mathbb{R}$ for all $d$ coordinates. i.e.
    $$
    \hat p(x) = \frac{1}{nh^d} \sum_{i=1}^n \kappa\left(\frac{x-X_i}{h}\right).
    $$
    

2. **Vector bandwidth (coordinate-wise bandwidth)**:

    If the density has different smoothness along different coordinates, then setting a scalar bandwidth might not provide good result. To account for the problem, vector bandwidth use $h_j\in\mathbb{R}$ for $j$-th coordinates, $j=1,\cdots,d.$
    

    $$
    \hat p(x) = \frac{1}{n\prod_{j=1}^d h_j} \sum_{i=1}^n \kappa\left(\frac{x_1-X_{i1}}{h_1}, \cdots, \frac{x_d-X_{id}}{h_d} \right).
    $$
    

3. **Bandwidth matrix**:

    In order to further account for possible rotation of the density contour, we can use a bandwidth matrix $H \in \mathbb{R}^{d\times d}$ so that our estimate be

    

    $$
    \hat p(x) = \frac{1}{n|H|} \sum_{i=1}^n \kappa\left( H^{-1} (x-X_i) \right).
    $$
    

Throughout this post, we will only focus on multivariate KDE cases with **product kernel function** and **coordinate-wise bandwidth**.

<br>

## Error analysis

<div class="theorem" text="bias expansion">

Suppose conditions (A3') and (A4) hold.

(A3'): $p$ is $2$-times partially continuously differentiable at $x,$ and $\frac{\partial^2}{\partial x_j \partial x_k} p(x)$ is integrable for all $j,k.$ <br>

(A4): $|u|^3 K(u) \to 0$ as $|u|\to\infty,$ $\int u^2 K(u) du < \infty,$ $\int K = 1,$ $K$ is symmetric.<br>

Then,
$$
E\hat p(x) - p(x) = \frac{1}{2}\mu_2(K) \sum_{j=1}^d h_j^2 \frac{\partial^2}{\partial x_j^2}p(x) + o\left( \sum_{j=1}^d h_j \right).
$$
</div> 

<br>

(A3') is a multivariate version of [(A3) that was discussed earlier](/non-parametric/Nonparametric-2-Univariate-Kernel-Density-Estimation#error-analysis-1), and (A4) is the same as before.

<br>

<div class="proof"><br>
$$
\begin{aligned}
E\hat p(x)
 &= \kappa_h * p(x) \\
 &= \int \frac{1}{h_1}K\left( \frac{x_1-u_1}{h_1} \right) \cdots \frac{1}{h_1}K\left( \frac{x_d-u_d}{h_d} \right) p(u_1,\cdots,u_d) d\mathbf{u} \\
 &= \int \prod_{j=1}^d K(w_j) p(x_1-w_1h_1,\cdots,x_d-w_dh_d)d\mathbf{w} \\
 &= p(x) + \int \prod_{j=1}^d K(w_j) \sum_{j=1}^d\left[ \frac{\partial}{\partial x_j} p(x) \cdot (-h_jw_j) \right] d\mathbf{w} + R\big(p(x)\big) + o\left( \sum_{j=1}^d h_j^2 \right) \\
 &= p(x) + R\big(p(x)\big) + o\left( \sum_{j=1}^d h_j^2 \right)
\end{aligned} \tag{1}
$$



The second equality is by substitution $w_j=\frac{x_j-u_j}{h_j},$ and the third follows from the first order Taylor expansion. Here, $R\big(p(x)\big)$ can be organized as follows, thus we get the desired result.
$$
\begin{aligned}
R\big(p(x)\big)
 &= \frac{1}{2} \sum_{j=1}^d \sum_{k=1}^d \left( \frac{\partial^2}{\partial x_j \partial x_k} p(x) h_jh_k\int w_jw_k\prod_{j=1}^d K(w_j) d\mathbf{w} \right) \\
 &= \frac{1}{2} \sum_{j=1}^d \left( \frac{\partial^2}{\partial x_j^2 p(x)} h_j^2 \int w_j^2 K(w_j) dw_j \right) \\
 &= \frac{1}{2} \mu_2(K) \sum_{j=1}^d h_j^2 \frac{\partial^2}{\partial x_j^2} p(x).
\end{aligned}
$$
</div> 

<br>

<div class="theorem" text="variance">

Suppose (A5) and (A6) hold.<br>

(A5): $p$ is continuous at $x.$ <br>

(A6): $|u|K(u) \to 0$ as $|u|\to\infty,$ $\int K^2 <\infty.$ <br>

Then,
$$
\text{Var}(\hat p(x)) = \frac{1}{n \prod_{j=1}^d h_j} \mu_0(K^2) p(x) + o\left(\frac{1}{n \prod_{j=1}^d h_j}\right).
$$


</div> 

<br>

Note that $\text{Var}(\hat p(x)) = \mathcal{O}\left( \frac{1}{n\prod_{j=1}^d h_j} \right).$ What it says, intuitively, is that the variance of multivariate KDE is reciprocal to the number of data inside *the region around the point $x$ that the kernel function looks for* (I would like to call it the **receptive field**[^1] of the kernel) when it estimates the density at $x.$

By similar arguments from univariate cases, we can derive the mean integrated squared error.

<Br>

<div class="theorem" text="MISE">

$p$: is $2$-time partiallly continuously differentiable on $\mathbb{R}^d,$ $\frac{\partial^2}{\partial x_j \partial x_k} p(x)$ is integrable for all $j,k$ and $p$ is square integrable. <br>

$K$: $\int u^2 K(u) du <\infty,$ $\int K = 1,$ $K$ is symmetric, $\int K^2 < \infty.$<br>

Then,
$$
\begin{aligned}
\text{MISE}(\mathbf{h})
 =~& \frac{1}{4} \mu_2(K)^2 \int \left( \sum_{j=1}^d h_j^2 \frac{\partial^2}{\partial x_j^2} p(x) \right)^2 dx \\
  &+ \frac{1}{n \prod_{j=1}^d h_j} \mu_0(K^2) p(x) \\
  &+ o\left( \sum_{j=1}^d h_j^2 + \frac{1}{n \prod_{j=1}^d h_j}\right).
\end{aligned}
$$
</div> 

<br>

The optimal $h_\text{opt}$ is the one that makes the first and second terms of MISE to have the same order. Letting 


$$
n^{-1} h_j^{-d} \sim h_j^4,~ j=1,\cdots,d,
$$




yields


$$
h_{j, \text{opt}} \sim n^{-1/(d+4)}. \tag{2}
$$


<br>

## Optimal bandwidth

### Coordinate-wise scaling

One method for finding optimal bandwidth is to use the result (2) and assume that 


$$
h_j = c_j \cdot n^{-1/(d+4)}.
$$


That is, each coordinate-wise bandwidth $h_j$ is a scalar multiple of another. As before, letting the first and second term of MISE to be the same, we get the system of $d$ equations:


$$
\int \left( \sum_{k=1}^d c_k^2 \frac{\partial^2}{\partial x_k^2} p(x) \right) \left( c_j^2 \frac{\partial^2}{\partial x_j^2} p(x) \right) dx = \frac{\mu_0(K^2)}{\mu_2(K)} \left(\prod_{j=1}^d c_j\right)^{-1},~ 1\le j\le d. \tag{3}
$$


Solve the equation and let $h_{j, \text{opt}} = c_{j, \text{opt}}\cdot n^{-1/(d+4)}.$

<br> 

### Global scaling

However, the equation (3) cannot be explicitly solved. To get the idea of the constant $c,$ we fallback to the scalar bandwidth


$$
h_\text{opt} = c_\text{opt} \cdot n^{-1/(d+4)}
$$


where $c_\text{opt}$ is the solution of the equation (3) with $c=c_j$ for all $1\le j\le d.$ This time we can explicitly get the solution


$$
c_\text{opt} = \left( \frac{d \cdot \mu_0(K^2)}{\mu_2(K)^2 \int \left( \sum_{j=1}^d \frac{\partial^2}{\partial x_j^2} p(x) \right)^2 dx} \right)^{1/(d+4)}.
$$


<br>

## Bandwith selection

As in the univariate cases, we need to select $\hat h$ that best acts the optimal $h.$ Recall that the LSCV selector is defined as 


$$
\text{LSCV}(\mathbf{h}) = \int \hat p(x)^2 dx - \frac{2}{n} \sum_{i=1}^n \hat p_{-i}(X_i).
$$


However, full-dimensional minimization of LSCV is intractable. We use coordinate-wise approach to avoid the problem.

### Bandwidth shrinkage

Bandwidth shrinkage scheme uses a minimizer of marginal $p_j(x_j)$ to infer $\hat h_j.$



1. **Minimize marginal.**

    For each $j,$ let $\hat h_j^\text{mg} = \argmin_{h>0} \text{LSCV}\_j(h_j),$ where $\text{LSCV}\_j = \int \hat p_j(x_j)^2 dx_j - \frac{2}{n} \hat p_{-i,j}(X_{ij}).$

2. **Grid search a global scaler.**

    Let $\hat \alpha = \argmin_{\alpha \in \mathcal{G}} \text{LSCV}(\alpha \hat h_1^\text{mg}, \cdots, \alpha \hat h_d^\text{mg}),$ where $\mathcal{G} \subset \mathbb{R}$ is a finite grid.

3. Let $\hat h_j = \hat \alpha \cdot \hat h_j^\text{mg}$ be our bandwidth.



### Coordinate-wise bandwidth selection

Coordinate-wise bandwidth selection (CBS) is simply a coordinate descent algorithm for LSCV. Instead of minimizing marginals, CBS minimizes conditional joints.



1. **Initialize.**

    Choose $\left( \hat h_1^{(0)}, \cdots, \hat h_d^{(0)} \right)$ from a finite grid $\mathcal{G}_1 \times \cdots \times \mathcal{G}_d \subset \mathbb{R}^d.$

2. **Coordinate descent until convergence.**
    
    $$
    \hat h_1^{(t+1)} = \argmin_{g_1 \in \mathcal{G}_1} \text{LSCV}\left( g_1, \hat h_2^{(t)}, \cdots, \hat h_d^{(t)} \right), \\
    \hat h_2^{(t+1)} = \argmin_{g_2 \in \mathcal{G}_2} \text{LSCV}\left( \hat h_1^{(t+1)}, g_2, \cdots, \hat h_d^{(t)} \right), \\
    \vdots \\
    \hat h_d^{(t+1)} = \argmin_{g_d \in \mathcal{G}_d} \text{LSCV}\left( \hat h_1^{(t+1)}, \hat h_2^{(t+1)}, \cdots, g_d \right).
    $$



<br>

## Curse of dimensionality

The optimal MISE under the assumption $h_j = c_j \cdot n^{-1/(d+4)}$ is 


$$
\inf_{\mathbf{h}>0} \text{MISE}(\mathbf{h}) \sim n^{4/(d+4)}.
$$


As $d$ increases, the error deteriorate fast. This is because the receptive field $r_\kappa(x)$[^1] of $\kappa$ around $x$ is defined as


$$
r_\kappa = \prod_{j=1}^d \left[ x_j - c_jh_j,~ x_j + c_jh_j \right],
$$


the volume of it is proportional to $\prod_{j=1}^d h_j,$ which goes to zero exponentially fast as $d \to \infty.$ Since using the the concept of receptive field as in univariate cases are useless in high-dimensional setting, we shoud think of other methods.

<br>

### Multiplicative model

Assume that the density is multiplicative.


$$
\hat p(x) = \prod_{j=1}^d f_j(x_j),~ x \in S \subset \mathbb{R}^d.
$$


This can be viewed as assuming that $p$ is a product of marginals. If $S$ is rectangular, the problem becomes solving $d$ different univariate KDE problems.

<br>

### Projection pursuit density estimation

PPDE estimates the density by projecting the data into lower-dimensional space, and feeding it to a multiplicative-like model. Friedman, Stuetzle and Schroeder (1984) described that "it attempts to overcome the curse of dimensionality by extending the classical univariate density estimation methods to higher dimensions in a manner that involves only univariate estimation."

PPDE is defined as 


$$
\hat p_{d_1}(x) = \hat p_0(x) \prod_{j=1}^{d_1} f_j(\beta_j^\intercal x),
$$


where $\hat p_0$ is a known initial guess, $\beta_j \in \mathbb{R}^{d_1},$ $d_1 \le d$ and $f_j$ is a univariate function. Again quoting the authors, "PPDE is seen to approximate the multivariate density by an initially proposed density $\hat p_0,$ multiplied (augmented) by a product of univariate functions $f_m$ of linear combinations $\beta_j\cdot x$ of the coordinates." $\hat p_0$ should be prespecified by the user, and PPDE's goal is to choose the projections $\beta_j$'s and functions $f_j$'s. The model can be reorganized into recursive form:


$$
\hat p_{d_1} = \hat p_{d_1 - 1} \cdot f_{d_1}(\beta_{d_1}^\intercal x).
$$


Thus PPDE can be seen as a process of adjusting the initial guess $\hat p_0$ with information from each coordinate $\beta_j^\intercal x$ using the augmenting function $f_j.$



<br>

***References***

* **Nonparametric Function Estimation (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Byeong U. Park).
* Friedman, Stuetzle and Schroeder. 1984. **Projection Pursuit Density Estimation**. Journal of the American Statistical Association. 79: 387. pp599-608.



[^1]: These are not formal expressions.

