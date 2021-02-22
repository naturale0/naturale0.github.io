---
layout: post
title:  "Borel-Cantelli lemmas are converses of each other"
date:   2020-04-29 15:11:00 +0900
author: "Sihyung Park"
categories: probability
---

<div class="theorem" text='Borel-Cantelli lemmas'>
(1) Let $A_n$ be a sequence of events. If $\sum\limits_{k=1}^\infty P(A_k) < \infty$, then $P(A_n \:\: i.o) = 0$.
<br>
(2) If $A_n$'s are independent, $\sum\limits_{k=1}^\infty P(A_k) = \infty$, then $P(A_n \:\: i.o) = 1$
</div>

<div class="proof">
(1) Let $N := \sum\limits_{k=1}^\infty \mathbf{1}_{A_k}$. The given condition implies $E(N)<\infty$, and thus $P(N<\infty)=1$. Hence at most finitely many $\mathbf{1}_{A_k}$'s should be $1$, and this is equivalent to $P(A_n \:\: i.o) = 0$
<br>
(2)
\begin{align*}
    P(\bigcap\limits_{k \geq m}{A_k}^c) &= \prod\limits_{k \geq m}\big( 1-P({A_k}) \big) \\
    &\leq \prod\limits_{k \geq m}e^{-P(A_k)} = e^{-\sum\limits_{k \geq m} P(A_k)} = 0, \:\: \forall m>0
\end{align*}
$\therefore P(\bigcup\limits_{k \geq m}{A_k}) = 1$ and $P(\limsup\limits_n{A_n}) = P(A_n \:\: i.o.) = 1$.
</div>

<div class="theorem" text="Kolmogorov's 0-1 law">
If $X_1, X_2, \cdots$ are independent, $A \in \mathcal{T}$, where $\mathcal{T} := \bigcap\limits_{k\geq1} \sigma(X_k, X_{k+1}, \cdots)$, then $P(A)=0$ or $1$.
</div>

<div class="proof">
Let $A \in \sigma(X_1, \cdots, X_k)$ and $B \in \sigma(X_{k+1}, \cdots, X_{k+j})$ for some $j$. Because $X_i$'s are independent, $A \perp B$. Thus $\sigma(X_1, \cdots, X_k) \perp \bigcup_j \sigma(X_{k+1}, \cdots, X_{k+j})$. Since both are $\pi$-systems, by Dynkin's $\pi$-$\lambda$ theorem,
\begin{equation}
    \sigma(X_1, \cdots, X_k) \perp \sigma(X_{k+1}, \cdots)
\end{equation}

Now, let $A \in \sigma(X_1, \cdots, X_j)$ for some $j$ and $B \in \mathcal{T} \subset \sigma(X_{j+1}, \cdots)$. By (1) and similar process, 
\begin{equation}
    \sigma(X_1, \cdots) \perp \mathcal{T}
\end{equation}

By (2), since $\mathcal{T} \subset \sigma(X_1, \cdots)$, $\mathcal{T}$ is independent of itself. <br>
$\therefore  A \in \mathcal{T} \to P(A) = P(A \cap A) = P(A)P(A)$.
</div>


Borel-Cantelli lemmas are widely used to prove almost sure convergence/existence of limit points of random variables. e.g. By showing that $P(\|X_n - X\|>\epsilon)$ is summable for any given $\epsilon > 0$, one can easily check almost sure convergence from convergence in probability.

Kolmogorov's 0-1 law shows that tail events (any $A \in \mathcal{T}$. $\mathcal{T}$ is called a "tail sigma-field") can only have either probability 0 or 1. Since $\\{A_n \\:\\: i.o\\}$ is a tail event, combined with Borel-Cantelli lemma, it is clear that the second Borel-Cantelli lemma is equivalent to the converse of the first one.



<div id="related" class="clearfix">
  <br><br>
<hr>
   <h3>Related Posts</h3>
  <ul>
    <li><a href="/probability/PTE-2.1-independence">(PTE) 2.1. Independence</a></li>
    <li><a href="/probability/PTE-2.3-B-C-lemmas">(PTE) 2.3. Borel-Cantelli lemmas</a></li>
    <li><a href="/probability/PTE-1.3-Random-variables">(PTE) 1.3. Random variables</a></li>
    <li><a href="/probability/PTE-1.1-Measure-theory">(PTE) 1.1. Basics on measure theory</a></li>
    <li><a href="/probability/PTE-4.2-martingales">(PTE) 4.2. Martingales and a.s. convergence</a></li>
  </ul>
</div>