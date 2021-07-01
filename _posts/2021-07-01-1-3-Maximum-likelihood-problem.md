---
layout: post
title: "1.3. Consistency of MLE"
date:   2021-07-01 16:23:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



The last example de Geer (2000) presents is the consistency of maximum likelihood estimates as the last example.[^1] Specifically, I would like to briefly prove Hellinger consistency of MLE provided that some form of law of large numbers holds.

The essential of this example is, *if we have a uniform law of large numbers then we can prove consistency of MLE even in a nonparametric setting*.



- TOC
{:toc}
<br> 

## (Pseudo) metrics for consistency

### Hellinger distance

Hellinger distance (or, Hellinger metric) is frequently used to show consistency of estimates. The metric $h$ is defined as a function of integrated squared difference of square roots of densities:


$$
h(p, q) := \left( \frac12 \int ( \sqrt p - \sqrt q )^2 d\mu \right)^{1/2},
$$


where $\mu$ is a measure dominating the distributions of $p$ and $q.$ 

<br>

### Kullback-Leibler divergence

Although it is *not* a metric[^2], the KL divergence $K(\cdot,\cdot)$ has been used extensively due to its relationship with metrics on a space of densities.


$$
K(p, q) := \int \log\frac{p(x)}{q(x)}p(x)d\mu(x),
$$


where $\mu$ is the dominating measure of the density $p.$ In other words, for a density indexed by $\theta,$


$$
K(p_{\theta_0}, p_\theta) = E_{\theta_0}\log\frac{p_{\theta_0}}{p_\theta}.
$$


The following fact shows that it suffices to show KL consistency in order to show Hellinger consistency.

<div class="lemma" text="relation between KL and Hellinger">
$$h^2(p_{\theta_0}, p_\theta) \le \frac 1 2 K(p_{\theta_0}, p_\theta).$$
</div> 

<div class="proof"><br>
The famous inequality
$$
\log x \le x -1 
$$
 is all we need for the proof.

</div> 



Hence we will show that the ULLN is a sufficiency of KL consistency.

<br>

## KL consistency of the MLE


$$
X \sim p_{\theta_0},~ \theta_0 \in \Theta
$$


where $p_{\theta_0}$ is a Radon-Nikodym density with respect to a $\sigma$-finite measure $\mu.$ Here, $\Theta$ can be either finite or infinite. Let $(X_i)_ {i=1}^n$ be a random sample from $p_{\theta_0}.$ Then


$$
\hat\theta_n := \argmax_{\theta\in\Theta} \sum_{i=1}^n \log p_{\theta}(X_i)
$$


is the MLE of $\theta_0$.

By definition, the following inequality holds[^3].


$$
\begin{aligned}
\text{(1)}&\; \sum_{i=1}^n \log\frac{p_{\theta_0}(X_i)}{p_{\hat\theta_n}(X_i)} \le 0 \\
\text{(2)}&\; E_{\theta_0} \log\frac{p_{\theta_0}(X)}{p_\theta(X)} \ge 0,~ \forall\theta\in\Theta
\end{aligned}
$$


It is convenient to define 


$$
g_\theta(\cdot)=\log\frac{p_{\theta_0}(\cdot)}{p_\theta(\cdot)},
$$


so that we can express $K(p_{\theta_0}, p_\theta) = Eg_\theta(X).$ It is clear by the strong law of large numbers that


$$
\left| \frac 1 n \sum_{i=1}^n g_{\theta}(X_i) - K(p_{\theta_0}, p_{\theta}) \right| \to 0 \text{ a.s.}
$$


Here, $\theta$ is fixed. Suppose the same result holds for a sequence $(\hat\theta_n)_ \{n\in\mathbb N\}.$ That is,


$$
\left| \frac 1 n \sum_{i=1}^n g_{\hat\theta_n}(X_i) - K(p_{\theta_0}, p_{\hat\theta_n}) \right| \to 0 \text{ a.s.} \tag{3}
$$




Using the inequality (1) coupled with this "uniform" strong law yields the result.



<div class="lemma" text="KL consistency of the MLE">
$$
\left| \frac 1 n \sum_{i=1}^n g_{\hat\theta_n}(X_i) - K(p_{\theta_0}, p_{\hat\theta_n}) \right| \to 0 \text{ a.s.} \\
\implies K(p_{\theta_0}, p_{\hat\theta_n}) \to 0 \text{ a.s.}
$$
</div> 

<div class="proof"><br>
$$
\begin{aligned}
0
 &\ge \frac1n\sum_{i=1}^n g_{\hat\theta_n}(X_i) \\
 &= \frac1n\sum_{i=1}^n g_{\hat\theta_n}(X_i) - K(p_{\theta_0}, p_{\hat\theta_n}) + K(p_{\theta_0}, p_{\hat\theta_n}).
\end{aligned}
$$

Therefore,
$$
\begin{aligned}
K(p_{\theta_0}, p_{\hat\theta_n}) 
 &\le \left| \frac 1 n \sum_{i=1}^n g_{\hat\theta_n}(X_i) - K(p_{\theta_0}, p_{\hat\theta_n}) \right| \\
 &\to 0 \text{ a.s. as } n \to \infty.
\end{aligned}
$$
</div> 

<br>

### Slower, but more obtainable rate

The ULLN (3) might not be easily obtainable, or might not even a fact in many cases. In this case, an extension of CLT can be used similarly as before.

We already know that


$$
\frac 1 {\sqrt n} \sum_{i=1}^n \big( g_\theta(X_i) - K(p_{\theta_0}, p_\theta) \big) \overset d \to \mathcal{N}\left(0, \text{Var}(g_\theta(X)) \right)
$$


which gives the rate


$$
\left| \frac 1 n \sum_{i=1}^n g_{\theta}(X_i) - K(p_{\theta_0}, p_{\theta}) \right| =\mathcal{O}_P(n^{-1/2}).
$$


Suppose the result holds for a sequence $(\hat\theta_n)_ \{n\in\mathbb N\}$:


$$
\left| \frac 1 n \sum_{i=1}^n g_{\hat\theta_n}(X_i) - K(p_{\theta_0}, p_{\hat\theta_n}) \right| =\mathcal{O}_P(n^{-1/2}).
$$


Then by the same argument, we can obtain KL - thus Hellinger - consistency of the MLE with the rate $\mathcal{O}_P(n^{-1/2}).$





<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).

<br>

[^1]: In fact, it is the second one but I switched the order to make things more clear.
[^2]: For those who are interested, [there is a metric derived from it](/information%20theory/a-metric-derived-from-KL-divergence).
[^3]: The left-hand side of the inequality (1) is sometimes referred to as the *empirical KL divergence*.