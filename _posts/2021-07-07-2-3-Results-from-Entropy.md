---
layout: post
title: "2.3. Entropy Inequalities"
date:   2021-07-07 14:08:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



This section covers the important results regarding the upper bound of entropies of popular classes of functions. We will accept most of the results without proving them, since it might obscure our objective: LLN and CLT on function spaces.

- TOC
{:toc}
<br> 

## For a class of functions $\mathcal G$

<div class="lemma" text="2.2">
Let $\mathcal X \subset \mathbb R$ be a finite set with cardinality $n.$ Let $\mathcal G = \{g:\mathbb R \to [0,1]~ \text{ is increasing}\}.$ Then
$$
H_\infty(\delta, \mathcal G) \le \frac 1 \delta \log\left( n + \frac 1 \delta \right),~ \forall \delta > 0.
$$
</div> 

<div class="proof"><br>
Given $\delta > 0.$ Suppose $\mathcal X = \{x_1\le\cdots\le x_n\}.$ For $g\in\mathcal G,$  define $M_i=\left\lfloor \frac{g(x_i)}{\delta} \right\rfloor$ and $\tilde g(x_i)=M_i\cdot\delta.$ Then
$$
|g(x_i) - \tilde g(x_i)| \le \delta,~ \forall x_i \in \mathcal X
$$
thus $\{\tilde g:~ g\in\mathcal G\}$ is a $\delta$-covering of $\mathcal G.$ Furthermore, by definition we get
$$
0\le M_1 \le \cdots \le M_n \le \lfloor 1/\delta \rfloor
$$
with $M_i\in\mathbb N$ for all $i$'s. The total number of $\tilde g$ corresponding to each $g\in\mathcal G$ is
$$
{ {n + \lfloor 1 / \delta \rfloor} \choose n } = { {n + \lfloor 1 / \delta \rfloor} \choose {\lfloor 1 / \delta \rfloor} }
$$
since it is the number of possible choices of $n$ samples out of population of size $\lfloor1/\delta\rfloor,$  regardless of orders but allowing for repititions. Hence,
$$
N_\infty(\delta,\mathcal G) \le \frac{\left(n+\lfloor1/\delta\rfloor\right)!}{\lfloor1/\delta\rfloor!~n!} = \left(\frac{n+\lfloor1/\delta\rfloor}{1}\right)^{1/\delta}.
$$
</div> 



<div class="theorem" text="entropy inequality 1">



<p>
    (1) (Birman and Solomjak, 1967)
    $$
    \mathcal G = \{g:\mathbb R \to [0,1] \text{ is increasing}\} \\
    \implies \exists A>0 \text{ s.t. } H_{B,2,Q}(\delta,\mathcal G) \le \frac 1 \delta A,~ \forall \delta >0,~ \forall Q.
    $$
</p>

<p>
    (2)
    $$
    \mathcal G = \{g:\mathbb R \to [0,1],~ \text{TV}(g)\le1 \} \\
    \text{ where } \text{TV}(g) := \int |dg| \\
    \implies \exists A>0 \text{ s.t. } H_{B,2,Q}(\delta,\mathcal G) \le \frac 1 \delta A,~ \forall \delta >0,~ \forall Q.
    $$
</p>
<p>
    (3) (lemma 2.3 of the text)
    $$
    \mathcal G = \{g:\mathbb [0,1] \to [0,1],~ \|g\|_\infty\le1 \} \\
    \implies \exists A>0 \text{ s.t. } H_\infty(\delta,\mathcal G) \le \frac 1 \delta A,~ \forall \delta >0.
    $$
</p>



<p>
    (4) (theorem 2.4 of the text)
    $$
    \mathcal G = \left\{g:\mathbb [0,1] \to [0,1],~ \int_0^1 \left|g^{(m)}(x)\right|^2 dx \le 1 \right\} \\ \text{(a Sobolev class)} \\
    \implies \exists A>0 \text{ s.t. } H_\infty(\delta,\mathcal G) \le \frac 1 {\delta^{1/m}} A,~ \forall \delta >0.
    $$
</p>


</div> 

<div class="proof"><br>
We will only prove the third result. Given $\delta>0,$ let 
$$
0=a_0<\cdots<a_N=1,~ a_k=k\delta,~ k=0,\cdots,N-1.
$$
Define $B_1=[a_0,a_1],$ $B_k=(a_{k-1},a_k],$ $k=2,\cdots,N.$ For $g\in\mathcal G,$ define
$$
\tilde g = \sum_{k=1}^N \delta\left\lfloor\frac{g(a_k)}{\delta}\right\rfloor\cdot\mathbf{1}_{B_k}
$$
as a step function. Then it is clear that $\|g-\tilde g\|_\infty \le \delta.$ Since $\tilde g$ is a step function on a finite number of intervals, to characterize $\tilde g$ for a fixed $g,$ we only need to specify the values $\tilde g(a_i)$ for $i=1,\cdots,N.$<br><br>

For $\tilde g(a_1)=\delta\cdot\lfloor g(a_1)/\delta \rfloor,$ there are at most $\lfloor1/\delta\rfloor+1$ choices (same as the proof of lemma 2.2). For $\tilde g(a_{k}),$ note the following inequality.
$$
\begin{aligned}
|\tilde g(a_k) - \tilde g(a_{k-1})|
 &\le |\tilde g(a_k) - g(a_{k})| + | g(a_k) - g(a_{k-1})| + |g(a_{k-1}) - \tilde g(a_{k-1})| \\
 &\le 3\delta.
\end{aligned}
$$
This is from the condition that $\|g'\|_\infty \le 1.$ Thus if $\tilde g(a_{k-1})$ is chosen,
$$
\tilde g(a_k) \in \left[\tilde g(a_{k-1}) - 3\delta,~ \tilde g(a_{k-1}) + 3\delta\right]
$$
so there are at most $7$ choices for $\tilde g(a_{k}).$<br><br>

From these, we get
$$
\begin{aligned}
N_\infty(2\delta,\mathcal G) 
 &\le \left( \left\lfloor \frac1\delta \right\rfloor + 1 \right)\cdot7^{\lfloor 1 / \delta \rfloor}, \\
H_\infty(2\delta,\mathcal G) 
 &\le \log\left( \left\lfloor \frac1\delta \right\rfloor + 1 \right) + \log7\cdot \left\lfloor\frac1\delta\right\rfloor \\
 &\le (\log7 + 1)\cdot \left(\frac1\delta+1\right).
\end{aligned}
$$
The last inequality is from $\log(1+x)\le x.$

</div> 

<br>



## For a subset $\mathcal G$ of a finite-dimensional space

<div class="lemma" text="2.5">
Let $B_d(r)=\{x\in\mathbb R^d:~ \|x\| \le r\},$ where $\|\cdot\|$ is the Euclidean norm. Then
$$
N(\delta, B_d(r), \|\cdot\|) \le \left( \frac{4r + \delta} \delta \right)^d,~ \forall \delta > 0.
$$
</div><br>



The lemma allows us to easily compute the $\delta$-entropy of a function class spanned by finite-dimensional basis.

<div class="corollary" text="2.6">

Let $\varphi_1,\cdots,\varphi_d \in L^2(Q)$ and 
$$
\mathcal G = \left\{ g=\sum_{i=1}^d\theta_i\varphi_i:~ \mathbf\theta=(\theta_1,\cdots,\theta_d)^\intercal\in\mathbb R^d,~ \|g\|_{2,Q}\le r \right\}.
$$
Then
$$
H_{2,Q}(\delta,\mathcal G) \le d\log\left( \frac{4r+\delta}\delta \right),~ \forall \delta>0.
$$


</div> 





<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).





