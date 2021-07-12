---
layout: post
title: "3.4.3. Uniform Law of Convex Hulls"
date:   2021-07-12 16:14:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



The last example of the ULLN that van de Geer (2000) present regards the convex hull of a function class. Take this subsection as a cherry on top.

- TOC
{:toc}
<br> 

## Convex hull

The convex hull $\text{conv}(\mathcal H)$ of a function class $\mathcal H$ is defined as the set of all finite convex combinations of functions in $\mathcal H.$ That is,


$$
\text{conv}(\mathcal H) = \left\{ \sum_{j=1}^r \theta_jh_j:~ h_j \in \mathcal H,~ \theta_j \ge 0,~ \sum_{j=1}^r \theta_j = 1,~, 1\le j\le r,~ r\in\mathbb N \right\}.
$$


<br>

## ULLN of convex hulls

In fact, deriving the uniform law of convex hulls does not utilize entropy inequality at all if the corresponding function class satisfies the ULLN.

<div class="lemma" text="3.13">
Suppose that $\mathcal H \subset L^1(P)$ satisfies the ULLN. Then $\text{conv}(\mathcal H)$ satisfies the ULLN as well.

</div> 

<div class="proof"><br>
Given $r\in\mathbb N,$ arbitrarily take $\theta_j \ge 0,$ $h_j \in \mathcal H$ for $1\le j\le r.$ Then
$$
\begin{aligned}
&\left| \int \sum_{j=1}^r \theta_j h_j d(P_n-P) \right| \\
 &= \left| \sum_{j=1}^r \theta_j \int h_jd(P_n-P) \right| \\
 &\le \cancel{\left(\sum_{j=1}^r \theta_j\right)}^1 \max_{1\le j\le r}\left|\int h_jd(P_n-P)\right|.
\end{aligned}
$$
Since $\mathcal H$ satisfies the ULLN, the right-hand side approaches zero as $n$ goes to infinity.

</div> 

<br>

## Convex hull inside the unit ball in $L^2$

For a more sophisticated argument, we do need help of entropy inequality.

<div class="theorem" text="3.14">

Let $Q$ be a probability measure on $(\mathcal X, \mathcal A)$ and $\mathcal H \subset B_{L^2(Q)}(0, 1)$ where $B_{L^2(Q)}(0, 1)=\{h:~\int h^2dQ\le 1\}.$ Then
$$
N_{2,Q}(\delta, \mathcal H) \le c\frac1{\delta^d},~ \forall \delta>0 \\
\implies \exists A(c,d)=A \text{: }~ H_{2,Q}(\delta, \text{conv}(\mathcal H)) \le A \frac{1}{\delta^{2d/(2+d)}},~ \forall \delta>0
$$
</div> 



The proof is in Ball and Pajor (1990).

<br>

### Example: A function class as a convex hull

Consider the [function class $\mathcal G$ from the first case of the entropy inequality 1](/2021/07/07/2-3-Results-from-Entropy#for-a-class-of-functions-mathcal-g):


$$
\mathcal G = \{g:\mathbb R\to[0,1] \text{ is increasing}\}.
$$


Notice that $\mathcal G \sub B_{L^2(Q)}(0,1)$ and is in fact for $\mathcal H = \{\mathbf 1_{[y,\infty)}:~ y\in\mathbb R\},$


$$
\mathcal G = \overline{\text{conv}}(\mathcal H).
$$


 i.e. is a closure of the convex hull of $\mathcal H.$ Given $\delta>0,$ let


$$
\mathcal Y_\delta=\{y_0, y_1,\cdots, y_{N-1}, y_N\}, \\
y_0 = Q^{-1}(\delta^2),~ y_N=Q^{-1}(\delta^2), \\
Q([y_{i-1},y_{i})) \le \delta^2,~ 1\le i\le N
$$


where $Q^{-1}(p)$ is the $(p\times100)$-percentile number of the probability measure $Q.$ Then it is clear that $\\{\mathbf 1_ {[y,\infty)}:~ y\in\mathcal Y_ \delta\\}$ is a $\delta$-covering. Thus for some constant $c,$ we have


$$
N_{2,Q}(\delta, \mathcal H) \le c\frac1{\delta^2}, ~\forall \delta >0
$$


Hence by theorem 3.14, for some constant $A$ depending only on $c,$ we get the entropy bound


$$
H_{2,Q}(\delta,\mathcal G) \le A\frac1\delta,~ \forall \delta>0
$$


since the closure does not affect the covering number. Compare this to the result (1) of entropy inequalities 1.



<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).