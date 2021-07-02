---
layout: post
title: "2.1. Empirical Process"
date:   2021-07-02 12:13:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



Chapter 2 concerns essential notions of the field. First, we will define the empirical distribution and the empirical process of a random sample. Next, various kinds of entropies and their basic relationships will be covered. Finally,  upper bounds of entropy of some of the function classes will be mentioned.

- TOC
{:toc}
<br>



## The Uniform Law of Large Numbers

Let $X_1,X_2, \cdots \overset {\text{indep.}}\sim P$ be i.i.d. copies of a random variable $X \sim P$ in $(\mathcal{X}, \mathcal{A}).$ Let $\mathcal{G} =\\{g_\theta:\theta\in\Theta\\}$ be a class of functions on $\mathcal X$ indexed by $\theta\in\Theta.$ We define the uniform law of large numbers (ULLN) as follows.

<div class="definition" text="the uniform law of large numbers"><br>
$\mathcal G$ satisfies the uniform law of large numbers, if
    $$
    \sup_{g\in\mathcal G} \left| \frac1n \sum_{i=1}^n g(X_i) - Eg(X) \right| \to 0 \text{ a.s.}
    $$
</div> 



If the ULLN holds, then the following clearly holds which was a sufficiency for the results of previous chapter such as MLE consistency.


$$
\left| \frac1n \sum_{i=1}^n g_{\hat\theta_n}(X_i) - Eg_{\hat\theta_n}(X) \right| \to 0 \text{ a.s.}
$$


<br>

## Empirical distribution

To grasp the essential of the ULLN, we simplify the formula by defining $P_n,$ the empirical distribution (or the empirical probability measure) of $P.$

[TBD]

<div class="definition" text="empirical distribution"><br>
</div> 





<br>

## Empirical process











