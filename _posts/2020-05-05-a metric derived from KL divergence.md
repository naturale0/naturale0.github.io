---
layout: post
title:  "A metric derived from KL divergence"
date:   2020-05-05 01:37:00 +0900
author: "Sihyung Park"
categories: [information theory]
---

<div class="definition" text="Kullback-Leibler divergence">
For probability densities $p_0$ and $p_1$, KL divergence of $p_1$ from $p_0$ is defined as $K(p_0, p_1) = -E_0(\log \frac{p_1(X)}{p_0(X)})$, where $E_0$ is an expectation with respect to $p_0$.
</div>

KL divergence is regarded as *"a distance"* between the two probability distributions. However, it is not a metric in mathematical sense, since $K(p_0, p_1) \neq K(p_1, p_0)$ in general.

What if we define a new function $D(p_0, p_1) := \frac{K(p_0, p_1) + K(p_1, p_0)}{2}$? It is easy to show from properties of KL divergence that 

$$\begin{align}
&\text{(1)} \:\: D \geq 0 \\
&\text{(2)} \:\: D(p_0, p_1) = D(p_1, p_0) \\
&\text{(3)} \:\: D(p_0, p_1) = 0 \iff p_0 = p_1   \\
\end{align}$$

However it is still not a metric since it is not necessarily true that the triangle inequality

$$\begin{align}
&\text{(4)} \:\: D(p_0, p_1) \leq D(p_0, p_2) + D(p_2, p_1)   \\
\end{align}$$

holds.

By setting up a reference density $M := \frac{p_0 + p_1}{2}$, and taking a square root, 

$$J(p_0, p_1) := \sqrt{\frac{K(p_0, M) + K(p_1, M)}{2}}$$

has been proven to satisfy triangule inequality. $J$ here is actually a square root of [Jensen-Shannon divergence](https://en.wikipedia.org/wiki/Jensen–Shannon_divergence) $JS(p_0, p_1)$.


Hence we can say that $J := \sqrt{JS}$ is truely **a metric defined on a set of density functions**.





 