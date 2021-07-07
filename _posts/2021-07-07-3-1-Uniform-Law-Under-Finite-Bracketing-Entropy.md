---
layout: post
title: "3.1. Uniform Law Under Finite Bracketing Entropy"
date:   2021-07-07 16:28:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



In Chapter 3, we will focus on the uniform law of large numbers and its sufficiencies. The first part of the chapter consists of the simplest case: ULLN under finite bracketing entropy condition. After that, techniques to prove sufficiencies of ULLN will be introduced. Finally, ULLN under limiting $L^1$-entropy, popular function classes, or under constraints in VC dimension will be covered.



- TOC
{:toc}
<br> 

## ULLN under finite bracketing entropy

The first form of the ULLN can be derived from finite bracketing entropy condition.

<div class="lemma" text="3.1. ULLN under finite bracketing entropy">

$$
H_{B,1,P}(\delta,\mathcal G),~ \forall \delta >0 \implies \mathcal G \text{ satisfies the ULLN.}
$$

</div> 

<div class="proof"><br>
Given $\delta>0.$ Let $\{[\ell_i,u_i]\}_{i=1}^N$ be a set of $\delta$-brackets for $\mathcal G.$
$$
\begin{aligned}
\int g d(P_n-P) 
 &le \int u_i dP_n - \int g dP \\
 &= \int u_i d(P_n-P) + \int (u_i-g) dP \\
 &\le \int u_id(P_n-P) + \delta.
\end{aligned}
$$
Similarly,
$$
\int gd(P_n-P) \ge \int \ell_id(P_n-P) - \delta.
$$
Hence,
$$
\begin{aligned}
\left| \int g d(P_n-P) \right|
 &\le \max\left\{ \int\ell_id(P_n-P), \int u_id(P_n-P) \right\} + \delta. \\
\sup_{g\in\mathcal G}\left| \int g d(P_n-P) \right|
 &\le \max_{i=1,\cdots,N}\left\{ \int\ell_id(P_n-P), \int u_id(P_n-P) \right\} + \delta. \\
\end{aligned}
$$
By Glivenko-Cantelli theorem, $\int \ell_i dP_n$ converges to $\int \ell_i dP$ almost surely for all $i$'s. Since the indices are finite, 
$$
\max_{i=1,\cdots,N}\left\{ \int\ell_id(P_n-P), \int u_id(P_n-P) \right\} \le \delta
$$
for sufficiently large $n.$ Hence
$$
\limsup_n \sup_{g\in\mathcal G} \left| \int g d(P_n-P) \right| \le 2\delta \text{ a.s.}
$$
and the result follows.

</div> 

<br>

## The envelope condition

<div class="definition" text="envelope"><br>
For a function class $\mathcal G,$ the function $G:=\sup_{g\in\mathcal G} |g|$ is the <b>envelope of $\mathcal G$</b>.<br>
In addition, we say $\mathcal G$ satisfies the <b>envelope condition</b>, if $G \in L^1(P).$
</div> 

In fact, the condition given in the lemma 3.1 is a sufficiency of the envelope condition.

<div class="lemma" text="sufficiency of the envelope condition">
$$
H_{B,1,P}(\delta,\mathcal G) < \infty,~ \forall\delta>0 \implies G \in L^1(P)
$$

where $G(x):=\sup_{g\in\mathcal G} |g(x)|.$

</div> 

<div class="proof"><br>
By the given condition, $\sup_{g\in\mathcal G}\|g\|_{1,P} < \infty.$ <br><br>

Let $\{[\ell_i,u_i]\}_{i=1}^N$ be a set of $1$-brackets of $\mathcal G.$ For $g\in\mathcal G,$ there exists an index $j$ such that $\ell_j \le g\le u_j.$ Because $|u_i-\ell_i|\le 1$ for all $i=1,\cdots,N,$
$$
\begin{aligned}
|g| &\le |u_j - \ell_j| + |\ell_j|, \\
\sup_{g\in\mathcal G} |g| &\le \sum_{i=1}^N |\ell_i| + \sum_{i=1}^N |u_i-\ell_i|.
\end{aligned}
$$
Hence,
$$
\|G\|_{1,P} \le \sum_{i=1}^N \|\ell_i\|_{1,P} + N < \infty.
$$
</div> 

​                                                                                

<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).