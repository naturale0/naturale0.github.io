---
layout: post
title:  "Determination of random variables and random number generation"
date:   2020-04-30 18:39:00 +0900
author: "Sihyung Park"
categories: probability
---

<div class="theorem" text='Distribution determines random variable'>
$F$ is a distribution of a random variable $X$, iff $F$ is (1) non decreasing, (2) right-continuous functions s.t. (3) $\lim\limits_{x\to -\infty}F(x) = 0$ and $\lim\limits_{x\to\infty}F(x) = 1$.
</div>

<div class="proof"> <br>
($\Rightarrow$) is trivial.
<br>
($\Leftarrow$) let $\Omega = [0, 1]$, $\mathcal{F} = \mathcal{B}\big( [0, 1] \big)$, $P=\lambda$ where $\lambda$ is a lebesgue measure. Define $X(\omega) := \sup\{y: F(y) < \omega\}$, then our claim is that X is a random variable that has $F$ as its distribution. To show the claim is true, we need to show 
$$P(X\leq x) = F(x) = P(\{\omega: 0\leq \omega \leq F(x)\})$$
which can be inferred by $\{\omega: X(\omega) \leq x\} = \{\omega: \omega \leq F(x)\}$, $\forall x$.
<br>
&ensp;
<br>

Given $x$, pick $\omega_0 \in \{\omega: \omega \leq F(x)\}$, since $F(x) \geq \omega_0$, $x \notin \{y: F(y) < \omega_0\}$. Therefore $X(\omega_0) \leq x$ and $\omega_0 \in \{\omega: X(\omega) \leq x\}$.
$$\begin{equation}
\therefore \: \{\omega: X(\omega) \leq x\} \supset \{\omega: \omega \leq F(x)\}, \forall x
\end{equation}$$

Given $x$, pick $\omega_0 \notin \{\omega: \omega \leq F(x)\}$, then $\omega_0 > F(x)$. Since $F$ is right-continuous, $\exists\epsilon > 0$ such that $F(x) \leq F(x+\epsilon) < \omega_0$. $x+\epsilon \leq X(\omega_0)$ because $X$ is defined as $\sup$, and this gives $x < X(\omega_0)$ and thus $\omega_0 \notin \{\omega: X(\omega) \leq x\}$.

$$\therefore \: \{\omega: X(\omega) \leq x\} \subset \{\omega: \omega \leq F(x)\}, \forall x$$

Hence the claim is true, and
$$\begin{align}
  F(x) &= \lambda\big( [0, F(x)] \big) = P(\{\omega: \omega \leq F(x)\})\\
       &= P(\{\omega: X(\omega) \leq x\}) = P(X \leq x)
\end{align}$$
</div>

<br>
<div class="theorem" text="Probability integral transform">
Suppose that a random variable $X$ has a continuous distibution $F$, then $Y := F(X) \sim \text{U}(0, 1)$
</div>

Probability integral transform can be proven by similar method to the one that used to prove theorem 1. The idea here is to construct a function that is an "inverse" of $F$. Since it is not sure that $F$ can have an inverse, it is safe to say that $X$ is constructed as an upper-quantile function of $F$.

The fact that we can naturally derive from here is interesting:

<div class="fact" text="inverse-transform sampling">
Suppose $U \sim \text{U}(0, 1)$. If a continuous distribution function $F$ has an inverse $F^{-1}$, then $X := F^{-1}(U) \sim F$.
</div>

So we can easily generate random numbers from continuous distribution with surjective CDF. For example, to generate random sample from exponential distribution with rate 1,

<div class="example" text="generating Exp(1) random sample">
1. Generate random numbers $u_i$'s from $\text{U}(0, 1)$.
<br>
2. $y_i := -\log(1-u_i)$ are random numbers from $\text{Exp}(1)$.
</div>


