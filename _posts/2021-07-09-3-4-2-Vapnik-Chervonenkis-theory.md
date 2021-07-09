---
layout: post
title: "3.4.2. Uniform Law of Vapnik-Chervonenkis Subgraph Classes"
date:   2021-07-10 01:51:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



In the previous article, results from lemma 3.1 were covered. Here, the uniform law for *Vapnik-Chervonenkis subgraph class*, a useful class of functions that has a close relationship with classification problem, will be derived from theorem 3.7.

- TOC
{:toc}
<br> 

## Vapnik-Chervonenkis class

Similar to various kinds of entropies, the Vapnik-Chervonenkis index (VC index, for short) is frequently used to measure complexity of sets of interest. 

<div class="definition" text="Vapnik-Chervonenkis class"><br>
Let $\mathcal D$ be a collection of subsets of $\mathcal X.$ Let $\xi_1,\cdots,\xi_n \in \mathcal X$ be fixed points on $\mathcal X.$

<p>
    (1) $$\Delta^\mathcal{D}(\xi_1,\cdots,\xi_n) := \text{Card}\left(\left\{D \cap \{\xi_1,\cdots,\xi_n\}:~ D\in\mathcal D\right\}\right)$$ is the number of subsets of $\{\xi_1,\cdots,\xi_n\}$ that can be selected using $\mathcal D.$
</p>



<p>
    (2) $$m^\mathcal{D}(n) := \sup_{x_1,\cdots,x_n\in\mathcal X}\left\{ \Delta^{\mathcal D}(x_1,\cdots,x_n) \right\}$$ is the supremum of $\Delta^{\mathcal D}$ that can be achieved by all possible sets in $\mathcal X$ of cardinality $n.$ If $\mathcal D$ can select all subsets of $\{\xi_1,\cdots,\xi_n\},$ then we say <b>$\mathcal D$ shatters $\{\xi_1,\cdots,\xi_n\}.$</b> 
</p>



<p>
    (3) $$V(\mathcal D) := \inf\{n:~ m^\mathcal{D} < 2^n\},$$ the minimal size of a set that is not shattered by $\mathcal D$, is the <b>Vapnik-Chervonenkis index of $\mathcal D.$</b>
</p>

<p>
    (4) $\mathcal D$ is a <b>Vapnik-Chervonenkis class</b>, if $V(\mathcal D) < \infty.$
</p>

</div>

 

For intuition, consider a "classification" (or should I say "separation" since there are only covariates) task. Suppose that $\mathcal X$ is a space of training data for classification problem and $\mathcal D$ is a collection of subsets of $\mathcal X$ that are consist of values of the same target class. Assume in addition that $\\{\xi_1,\cdots,\xi_n\\}$ is an unseen data. Then the VC index of $\mathcal D$ indicates plausibility or complexity of the task: 

* If $V(\mathcal D) = \infty,$ the problem cannot be solved completely using the training data. 
* If $V(\mathcal D)=k<\infty,$ the problem can be solved and it requires $k$-times to completely separate the unseen data in the worst case scenario.

Since the complete shattering of a set of cardinality $n$ requires $2^n$-times of separation, if $m^\mathcal{D}(n)$ grows polynomially in $n,$ (i.e. grows slower than exponential rate) $\mathcal D$ is a VC class.

For examples, one can show that the following classes are all VC classes.

1. $\mathcal D_1 = \\{(-\infty, t]:~ t\in\mathbb R\\} \subset \mathbb R.$ $\implies V(\mathcal D_1)=n+1.$
2. $\mathcal D_2 = \\{(-\infty, t]:~ t\in\mathbb R^d\\} \subset \mathbb R^d.$ $\implies V(\mathcal D_2)=(n+1)^d.$
3. $\mathcal D_3 = \left\\{ \\{ x:~ \theta^\intercal x > y \\}:~ \theta \in \mathbb R^d,~ y\in\mathbb R \right\\} \subset \mathbb R^d.$ $\implies V(\mathcal D_3)=d+2.$

<br>

## Vapnik-Chervonenkis subgraph class

VC index is for a **collection of subsets**. To fit VC theory into the theory of empirical process, we need to characterize functions by sets. Subgraph can be a choice.

<div class="definition" text="VC subgraph class"><br>
<p>
    (1) $$\text{sub.}f := \left\{ (x,y) \in {\mathcal X}\times{\mathbb R}:~ f(x) > y \right\}$$ is the <b>subgraph of a function $f:\mathcal\to\mathbb R.$</b>
</p>

<p>
    (2) $\mathcal G$ is a <b>Vapnik-Chervonenkis subgraph class</b> if $V(\mathcal G) < \infty,$ where $$V(\mathcal G) := V\left( \{\text{sub.}g:~ g\in\mathcal G\} \right)$$ is the VC index of $\mathcal G$
</p>

</div> 

As an example, consider again a class of functions with finite basis: 


$$
\mathcal G = \{\theta_1\psi_1+\cdots+\theta_d\psi_d:~ \boldsymbol\theta\in\mathbb R^d\}, \\
\psi_1,\cdots,\psi_d \text{ are fixed functions.} \tag{ex. 3.7.4d}
$$


Such $\mathcal G$ is a VC subgraph class with $V(\mathcal G) \le d+2$ (follows directly from the third example of VC class).

<br>

## ULLN of VC subgraph class

It is natural to relate VC theory with entropy. One can easily speculate that a VC subgraph class has a well-controlled entropy. The next lemma is a confirmation to this.

<div class="lemma" text="3.11">
If $\mathcal G$ is a VC subgraph class and $G(x)=\sup_{g\in\mathcal G}|g(x)|$ is the envelope of $\mathcal G,$ then there exists a constant $C$ such that 
$$
N_{p,Q}(\delta\cdot\|G\|_{p,Q}, \mathcal G) \le C\frac{V(\mathcal G)\cdot(16e)^{V(\mathcal G)}}{\delta^{p(V(\mathcal G)-1)}}, ~\forall \delta>0,~ \forall p<\infty,~ \forall \text{p.m. }Q
$$
</div> 



Here, $\text{p.m.}$ stands for "probability measure". Notice that the constant $C$ exists uniformly over every probability measures $Q$'s. By the vanishing random entropy condition, this, together with the envelope condition, implies the ULLN.



<div class="corollary" text="3.12. ULLN of VC subgraph class">
For a class of functions $\mathcal G,$ if the following conditions hold,

<p>
    (a) $\mathcal G$ is a VC subgraph class.
</p>

<p>
    (b) $G=\sup_{g\in\mathcal G}|g| \in L^1(P).$
</p>

then $\mathcal G$ follows the ULLN.

</div>

<div class="proof"><br>

$$
\frac1n H_{1,P_n}(\delta\cdot\|G\|_{1,P_n}) \le \frac1n \log\left( C\frac{V(\mathcal G)\cdot(16e)^{V(\mathcal G)}} {\delta^{p(V(\mathcal G)-1)}} \right) \to 0.
$$
</div> 

<br>

As an example, consider again the example 3.7.4d. Because the envelope is not integrable, for a probability measure $Q$ and $R>0,$ define


$$
\mathcal G_{R} = \{g\in\mathcal G:~ \|g\|_{2,Q} \le R\}.
$$


Suppose that the basis is in fact orthogonal. i.e. $\Sigma_Q = \int \Psi\Psi^\intercal dQ = \mathbf I_d$ where $\mathbf I_d \in \mathbb R^{d\times d}$ is an identity. Then we can derive two entropy bounds:

1. ([from corollary 2.6](/2021/07/07/2-3-Results-from-Entropy#for-a-subset-mathcal-g-of-a-finite-dimensional-space)) 

    $$H_{2,Q}(\delta, \mathcal G_R) \le A_1d\log\left( \frac R\delta \right)$$

2. (from corollary 3.12) 

    $$H_{2,Q}(\delta, \mathcal G_R) \le A_2d\log\left( \frac {dR}\delta \right)$$

The former is better since the logarithm is independent to dimension. 

<div class="proof" text="the latter bound"><br>

By the Cauchy-Schwarz inequality,
$$
G(x) = \sup_{g\in\mathcal G}|g(x)| = \|\Psi(x)\|_2 \cdot R.
$$
Hence
$$
\|G\|_Q = \sqrt d R.
$$
Now apply theorem 3.11.

</div> 



<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).