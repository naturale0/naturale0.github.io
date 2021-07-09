---
layout: post
title: "3.4. Examples of Sufficiencies of the Uniform Law"
date:   2021-07-09 15:33:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



The ULLN under finite bracketing entropy condition ([lemma 3.1](/2021/07/07/3-1-Uniform-Law-Under-Finite-Bracketing-Entropy#ulln-under-finite-bracketing-entropy)) and vanishing random entropy condition ([theorem 3.7](/2021/07/09/3-3-Uniform-Law-Under-Random-Entropy#theorem-37-main-theorem-l1-condition)) paves the way to the uniform law of frequently used function classes. Here, three examples from lemma 3.1 and one example from theorem 3.7 will be presented.

- TOC
{:toc}
<br> 

## Results from lemma 3.1

### 1. Class of monotone functions

Given a fixed function $F \ge 0,$ define the classese of interest.
$$
\tilde{\mathcal G} := \{\tilde g:\mathbb R\to\mathbb R \text{ is increasing},~ \|\tilde g\|_\infty \le 1\} \\
\mathcal G := \{\tilde g F:~ \tilde g \in \tilde{\mathcal G}\}
$$
Then the followings hold.

<div class="lemma" text="3.8">
<p>
    (1) For all $1\le p<\infty,$ there exists a constant $A>0$ such that 
    $$
    H_{B,p,Q}(\delta,\mathcal G) \le A\frac{\|F\|_{p,Q}}\delta,~ \forall \delta>0,~ \forall \text{ probability measure }Q
    $$
</p>

<p>
    (2) If $F \in L^1(P),$ then $\mathcal G$ satisfies the ULLN.
</p>

</div>

<div class="proof"><br>
(1) Let $[\tilde \ell, \tilde u]$ be a bracket of $\tilde{\mathcal G}.$ Then clearly $[\tilde \ell F, \tilde u F]$ is a bracket of $\mathcal G.$
$$
\begin{aligned}
&\int \left| \tilde u F - \tilde\ell F \right|^p dQ \\
&= \int \left| \tilde u - \tilde\ell \right|^p |F|^p dQ \\
&= \int \left| \tilde u - \tilde\ell \right|^p \frac{|F|^p}{\|F\|_{p,Q}^p} dQ \cdot \|F\|_{p,Q}^p \\
&= \int \left| \tilde u - \tilde\ell \right|^p d\tilde Q \cdot \|F\|_{p,Q}^p
\end{aligned}
$$
where $\tilde Q$ is a push-forward probability measure such that
$$
d\tilde Q := \frac{|F|^p}{\|F\|_{p,Q}^p} dQ.
$$
From this formulation, we get
$$
\|\tilde\ell F - \tilde u F\|_{p,Q} = \|\tilde\ell - \tilde u\|_{p,Q}\cdot \|F\|_{p,Q}.
$$
Hence,
$$
\begin{aligned}
&H_{B,p,Q}(\delta,\mathcal G) \\
&= H_{B,p,\tilde Q}(\delta/\|F\|_{p,Q}, \tilde{\mathcal G}) \\
&\le A\frac{\|F\|_{p,Q}}{\delta}.
\end{aligned}
$$
The last inequality is from the first result of <a href="/2021/07/07/2-3-Results-from-Entropy">entropy inequalities</a>.<br><br>

(2) The result (1) implies the bracketing entropy be finite. Apply lemma 3.1.

</div>  

<br>

### 2. The Sobolev-Hilbert class

For a fixed $m\in\mathbb N$ and $R>0,$ define **the Sobolev-Hilbert class of $m$**
$$
\mathcal G := \left\{ g:[0,1]\to\mathbb R,~ \int\left( g^{(m)}(x) \right)^2dx\le 1,~ \|g\|_{2,Q} \le R \right\}.
$$
Let
$$
\Sigma_Q := \int \Psi\Psi^\intercal dQ, \\
\Psi=(\psi_1,\cdots,\psi_m)^\intercal, \\
\psi_k(x) = x^{k-1},~ k=1,\cdots,m.
$$

<div class="lemma" text="3.9">
If $\Sigma_Q$ is invertible, then there exists a constant $A$ such that
$$
H_\infty(\delta,\mathcal G) \le A \frac{1}{\delta^{1/m}}
$$
so that the ULLN holds for $\mathcal G.$

</div> 

It suffices to show the condition of theorem 2.4. The proof uses the Taylor's theorem together with upper bound by eigenvalue so I will not cover it.

<br>

### 3. Class of functions parametrized by $\theta$

Consider a parameter space $\Theta$ which is a **compact metric space**. Let
$$
\mathcal G := \{g_\theta:~ \theta\in\Theta\}
$$
where the map $\theta \mapsto g_\theta$ is **continuous** for $P$-almost all $x$'s.

van de Geer (2000) mentions that the ULLN for this class is "more or less classical".

<div class="lemma" text="3.10">
Suppose the envelop condition $G := \sup_{\theta\in\Theta}|g_\theta|\in L^1(P)$ holds. Then
$$
H_{B,1,P}(\delta,\mathcal G) < \infty,~ \forall \delta>0
$$
so that the ULLN holds for $\mathcal G.$

</div> 

<div class="proof"><br>
Let $w$ be the modulus of continuity of $\mathcal G.$ That is,
$$
w(\theta,r)(x) := \sup_{\theta' \in B(\theta,r)} |g_\theta(x) - g_{\theta'}(x)|
$$
so that 
$$
\{g_{\theta'}:~ \theta'\in B(\theta,r)\} \subset [g_\theta-w(\theta,r),~ g_\theta+w(\theta,r)].
$$
By continuity of $\theta\mapsto g_\theta,$ $w(\theta,r) \to 0$ as $r\to0$ for $P$-almost all $x$'s. In addition,
$$
\begin{aligned}
|w(\theta,r)(x)|
 &\le \sup_{\theta'\in B(\theta,r)}|g_\theta(x)| + g_{\theta'}(x) \\
 &\le 2G(x) \in L^1(P)
\end{aligned}
$$
thus by the dominated convergence theorem,
$$
\int w(\theta,r)dP \to 0 \text{ as } r \to 0.
$$
Now, given $\delta>0,$ for all $\theta\in\Theta$ there exists $r_\theta$ such that
$$
\int w(\theta, r_\theta) < \delta.
$$
Hence $\{B(\theta,r_\theta):~ \theta\in\Theta\}$ is an open cover of $\Theta.$ Since $\Theta$ is compact, there exists a finite subcover $\{B(\theta_i, r_{\theta_i}\}_{i=1}^N$ and 
$$
\left\{ [g_{\theta_i}-w(\theta_i, r_{\theta_i}),~ g_{\theta_i}+w(\theta_i, r_{\theta_i})] \right\}_{i=1}^N
$$
becomes a $2\delta$-bracketing set of $\mathcal G,$ since
$$
\int \left( g_{\theta_i}+w(\theta_i, r_{\theta_i}) \right) - \left( g_{\theta_i}-w(\theta_i, r_{\theta_i}) \right) dP \\
=2\int w(\theta_i, r_{\theta_i}) dP \le 2\delta.
$$
 The proposed result directly follows.

</div> 



<br>

## Result from theorem 3.7

[TBD]













<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).