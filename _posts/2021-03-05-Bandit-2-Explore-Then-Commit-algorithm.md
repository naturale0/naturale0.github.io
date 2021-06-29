---
layout: post
title: "2. Explore-Then-Commit algorithm"
date:   2021-03-05 12:31:00 +0900
author: "Sihyung Park"
categories: [adaptive sequential decision making]
---



Here, we continue to describe the multi-armed bandit problem in detail. The notion of regret will be introduced. Then our first bandit algorithm, explore-then-commit (ETC) will be described.



- TOC
{:toc}
<br> 

## Multi-armed bandit (continued)

Suppose we have a set of possible actions $\mathcal{A}$ and a **stochastic bandit** (a collection of bandits) $\nu$ where


$$
\nu := (P_{\theta_i})_{i \in \mathcal{A}}.
$$


The algorithm interact with bandits through time $t=1,\cdots,T.$ At each time $t$ the algorithm choose an arm $a(t) \in \mathcal{A}.$ Then the reward $r_i(t) \sim P_{\theta_{a(t)}}$ is generated and revealed to the algorithm. Such interactions (action-reward pairs) between the algorithm and the environment is logged into history $\mathcal{H}$ where


$$
\mathcal{H}_{t-1} := \{\left(a(t), r(t)\right): t=1,\cdots,t-1\}.
$$


The algorithm can be characterized by a sequence of probabilities $(\pi_t)_{t=1,\cdots,T}.$ Arms are chosen according to conditional probability given history $\pi_t = \pi(\cdot\|\mathcal{H}\_{t-1}).$ Our goal is to find $(\pi_t)$ that chooses the best actions at each $t.$

Usually such problem is solved by not maximizing the cumulative reward, but by minimizing the **regret function** $R$. As the name implies, $R$ is the value that represents the total loss that we had under our choices. To formally define the regret, let $\mu_i$ be the (unknown) expected reward from the $i$th arm, and $\mu_{i^\*}$ be the expected reward from the (also unknown) best $i^\*$th arm.

$$
\mu_i = E r_i(t) \tag{1}, \\
\mu_{i^*} \ge \mu_j,~ \forall j \ne i^*.
$$


Let $\Delta_j$ be the difference between the mean reward from the best choice and the choice $j$.


$$
\Delta_j := \mu_{i^*} - \mu_j.
$$



The regret $R$ is defines as follows:


$$
\begin{aligned}
R(T)
 &:= E \sum_{t=1}^T \left( \mu_{i^*} - r_{a(t)}(t) \right) \\
 &= \sum_{t=1}^T \Delta_{a(t)}.
\end{aligned}
$$

<br>



## Exploration-exploitation trade-off

What makes the bandit problem so challenging is that only a small portion of rewards are revealed: we do not know underlying $P_{\theta_i}$'s unless we chose them to get enough samples. This problem is called **exploration-exploitation trade-off**. Simply put, we need to find *and* use the best among $\nu$ in limited amount of time $T.$

* Exploration: Try different arms to get information about $P_{\theta_i}.$
* Exploitation: Pick the best arm according to estimates of rewards based on current information about $P_{\theta_i}.$ 

One thing to note is that in exploitation, we not only need to get the estimate, but also the *variabiliy of it*.

<br>



## Theoretical tools

The followings are some of the tools that will be used in regret analysis.

### Markov and Chebeshev's inequality

<div class="theorem" text="Markov">
For a random variable $X \ge 0$ and $\epsilon > 0,$
$$
P(X \ge \epsilon) \le \frac{EX}{\epsilon}.
$$
</div> 



<div class="theorem" text="Chebyshev">

For a random variable $X$ and $\epsilon > 0,$
$$
P(|X - EX| \ge \epsilon) \le \frac{\text{Var}(X)}{\epsilon^2}.
$$
</div> 

<br>

### subgaussianity

<div class="definition" text="sub-gaussianity"><br>
A random variable $X$ is $\sigma$-subgaussian, if there exists a $\sigma>0$ such that 
$$
E e^{\lambda X} \le e^{\lambda^2\sigma^2/2}.
$$
That is, the MGF of $X$ is bounded above by another random variable that follows $\mathcal{N}(0,\sigma^2).$

</div> 

A $\sigma$-subgaussian $X$ can be viewed as a random variable that has tail probabilities smaller than that of $\mathcal{N}(0, \sigma^2).$ To be specific, the right tail probablity can be achieved by **Chernoff method**. Be careful since the bound is not tight for normal random variables.

<div class="theorem" text="Chernoff">

For a $\sigma$-subgaussian random variable $X,$
$$
P(X \ge \epsilon) \le e^{-\frac{\epsilon^2}{2\sigma^2}}.
$$
</div> 

<div class="proof"><br>
Let $\lambda = \epsilon / \sigma^2,$ then
$$
\begin{aligned}
P(X \ge \epsilon)
 &= P(e^{\lambda X} \ge e^{\lambda \epsilon}) \\
 &\le Ee^{\lambda X}/e^{\lambda \epsilon} \\
 &\le e^{\lambda^2\sigma^2/2}/e^{\lambda\epsilon} \\
 &= e^{-\frac{\epsilon^2}{2\sigma^2}}.
\end{aligned}
$$
The first inequality follows from Markov's inequality and the second follows from subgaussianity.

</div> 

Similarly the same inequality holds for the lower tail, thus we get the bound


$$
P(|X| \ge \epsilon) \le 2 e^{-\frac{\epsilon^2}{2\sigma^2}},
$$


which is (as we set $\delta = 2e^{-\frac{\epsilon^2}{2\sigma^2}}$) equivalent to 


$$
P\left(|X| \ge \sqrt{2\sigma^2 \log\left(\frac{2}{\delta}\right)}\right) \le \delta.
$$


<div class="lemma" text="5.4">

$X$ is $\sigma$-subgaussian, $X_1, X_2$ are $\sigma_1$- and $\sigma_2$-subgaussian, respectively. Then<br>

(i) $EX=0$ and $\text{Var}(X) \le \sigma^2.$<br>

(ii) $cX$ is $|c|\sigma$-subgaussian for all $c \in \mathbb{R}.$<br>

(iii) $X_1+X_2$ is $\sqrt{\sigma_1^2 + \sigma_2^2}$-subgaussian.

</div> 

With the help of the lemma, applying Chernoff bound to the sample mean $\hat \mu=\frac{\sum_{t=1}^T X_t}{T}$ of $\sigma$-subgaussian $X$ yields


$$
P(|\hat \mu - \mu| \ge \epsilon) \le 2 e^{-T\frac{\epsilon^2}{2\sigma^2}}.
$$


<br>

### Bernstein inequality

<div class="lemma">
If $P(|X| \le c) = 1$ and $EX=0,$ $\text{Var}(X)=\sigma^2,$ then for any $t>0,$
$$
Ee^{tX} \le \exp\left( t^2\sigma^2\frac{e^{tc} - 1 - tc}{(tc)^2} \right).
$$
</div> 

<div class="proof"><br>
$$
\begin{aligned}
Ee^{tX}
 &= E\left(1 + tX + \sum_{r=2}^\infty \frac{t^rX^r}{r!} \right) \\
 &= 1 + t^2\sigma^2F \\
 &\le e^{t^2\sigma^2F}
\end{aligned}
$$



where $F=\sum_{r=2}^\infty \frac{t^{r-2}}{\sigma^2} \frac{EX^r}{r!}.$ Since $EX^r \le c^{r-2}\sigma^2$ for $r\ge2,$ we get the desired result.

</div>

<div class="theorem" text="Bernstein">

Let $X_t$'s be independent random variables with $P(|X_t| \le c) = 1$ and $EX_i=0,$ $\sigma^2 = \sum_{t=1}^T \text{Var}(X_t).$ Then for any $\epsilon>0,$
$$
P(|\hat \mu| \ge \epsilon) \le 2 \exp\left( -\frac{T\epsilon^2}{2\sigma^2 + 2c\epsilon/3} \right).
$$
</div> 

<br>



## Explore-then-Commit (ETC)

### The algorithm

The first and probably the simplest form of the bandit algorithm is explore-then-commit (ETC). As the name speaks for it self, ETC divides total time $T$ into exploration step and exploitation step.

1. **Exploration step.** During rounds $1,\cdots,mN,$ the algorithm plays each $N$ arms $m$ times.

2. **Exploitation step.** The algorithm selects the arm with the highest empirical mean reward 

    $$
    a = \argmax_{i=1,\cdots,N} \hat \mu_i (mN)
    $$

    where

    
    $$
    \hat \mu_i(t) := \frac{\sum_{\tau=1}^t r_i(\tau) \mathbf{1}(i=a(\tau))}{\sum_{\tau=1}^t \mathbf{1}(i=a(\tau))}.
    $$

    During the rest $mN+1,\cdots,T$ rounds, the algorithm chooses that $a$. That is, $a(t) = a$ for all $t=mN+1,\cdots,T.$



Although the algorithm is simple, it is (quite predictively) not a great performing one. Choice of the exploration parameter $m$ depends on the underlying knowledge of $\Delta_i$'s, which is not available. In addition, the algorithm is suboptimal in regret analysis.

<br>

### Regret analysis

[To be appended]













<br>

***References***

* Lattimore, Szepesvari. 2020. **Bandit Algorithms**. Cambridge University .
* **Seminar in Recent Development of Applied Statistics (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Myunghee Cho Paik).