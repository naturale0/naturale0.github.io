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
$$P_n := \frac1n \sum_{i=1}^n \delta_{Xi}$$

is the empirical distribution based on $X_1,\cdots, X_n.$

</div> 

Here, $\delta_x$ is the dirac measure concentrated on $x.$ i.e. $\delta_x(z)=1$ if $x=z$ and $0$ otherwise. Notice that by defining the empirical version of the probability measure $P,$ we can express the uniform law as follows.


$$
\sup_{g\in\mathcal G} \left| \int g ~d(P_n-P) \right| \to 0 \text{ a.s.}
$$


<br>

## Empirical process

To state some uniform version of the central limit theorem, we define the empirical process. Recall that in our notation, the classical central limit theorem can be written as


$$
\sqrt n \int g~ d(P_n - P) \overset d \to \mathcal N(0, \sigma^2_g), \tag{1}
$$


where, for simplicity, the mean and the variance of $g(X)$ is written as


$$
m_\theta := Eg_\theta(X) = \int g_\theta(x)dP(x), \\
\sigma^2_g := \text{Var}(g(X)).
$$


Be careful that since $\hat\theta_n$ contains random component $X_1,\cdots,X_n$ in its definition, $m_{\hat\theta_n} = \int g_{\hat\theta_n(X_1,\cdots,X_n)}(z)dP(z)$ is <u>not</u> a constant. We define the empirical process of $X_1, X_2, \cdots$ so that it can extend (1) to be somewhat "uniform".



<div class="definition" text="empirical process"><br>
$$
    \left\{v_n(g) := \sqrt n \int g~ d(P_n-P) \right\}_{g \in \mathcal G}
$$
    is the empirical process indexed by $\mathcal G.$
</div> 

<br>



## Asymptotic equicontinuity

For an empirical process, there exists a slightly weaker condition than the central limit theorem, but a sufficiency for many cases. it is the *asymptotic equicontinuity.*



<div class="definition" text="asymptotic equicontinuity"><br>

$\{v_n(g)\}_{g \in \mathcal G}$ is asymptotically equicontinuous at $g_0 \in \mathcal G,$ if 
$$
|v_n(\hat g_n) - v_n(g_0)| = o_P(1),~ \forall \{\hat g_n\} \sub \mathcal G \text{ such that } \|\hat g_n - g_0\|_2 = o_P(1).
$$
</div> 



It is direct that the uniform version of the CLT holds for $\\{v_n(g)\\}_ {g\in\mathcal G}$ if it is asymptotically equicontinuous at $g_0,$ $\sigma_ {g_0} ^2$ is finite, and $\hat g_n$ approaches $g_0$ in probability.



<div class="lemma" text="(2.3) of p.15">
Suppose $\{v_n(g)\}_{g \in \mathcal G}$ is asymptotically equicontinuous at $g_0,$ $\sigma^2_{g_0} < \infty,$ and $\|\hat g_n - g_0\| = o_P(1)$ Then
                                                                                                                $$
v_n(\hat g_n) \overset d \to \mathcal N(0, \sigma_{g_0}^2).

$$                                                                                                                
</div> 

<div class="proof"><br>
$$
v_n(\hat g_n) = v_n(g_0) + o_P(1) \overset d \to \mathcal N(0, \sigma^2_{g_0}).
$$

</div> 





<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).