---
layout: post
title: "1.1. Binary choice model"
date:   2021-06-30 13:42:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



The first chapter of **Empirical Processes in M-estimation** (van de Geer, 2000) devotes to introduction to the field. To be specific, it introduces two main tools that will be used throughout the textbook: *the law of large numbers* and *the central limit theorem*.

But wait, didn't we already studied the two in probability theory? It turns out, in the empirical process theory, we want to study the asymptotics of estimates *on a function space*, not on a Euclidean space. This requires other types of the theorems, namely the uniform law of large numbers (ULLN) and the functional central limit theorem (Donsker's theorem; fCLT).

My major goal is to review the first four chapters of van de Geer (2000). This covers the theory of ULLN and its application to consistency. For the latter (fCLT) I would like to mention the basics of it when reviewing Billingsley (1999)[^2].



- TOC
{:toc}
<br> 

## Notation and Settings

Let $(\mathcal{X}, \mathcal{A})$ be a measurable space. Let $P$ be a probability measure on such space and $g: \mathcal{X} \to \mathbb R.$ Suppose we have a random sample


$$
X_1, \cdots, X_n \overset{\text{i.i.d.}} \sim P.
$$


As I briefly mentioned above, the two major theorems of probability theory is the strong law of large numbers and the central limit theorem.


$$
\begin{aligned}
\text{SLLN: }\;& E|g(X_1)| < \infty \implies \frac1n \sum_{i=1}^n g(X_i) \to Eg(X_1) \text{ a.s.} \\
\text{CLT: }\;& \sigma_g^2 := \text{Var}(g(X_1)) < \infty \implies \frac{1}{\sqrt{n}} \sum_{i=1}^n \big(g(X_i)-Eg(X_i)\big) \overset{d}{\to} \mathcal{N}(0,1)
\end{aligned} \tag{1}
$$


One important remark is that this results hold only for a fixed $g.$ Our interest from now on lies on the case where $g$ is not fixed.

Consider a class of functions $\mathcal{G} = \\{g_\theta: \mathcal{X} \to \mathbb R,~ \theta\in\Theta\\}$ indexed by a paramter $\theta$ in a metric space $\Theta.$ We want to prove or disprove that the result (1) holds uniformly on $\mathcal{G}.$ In addition, if (1) uniformly holds, then for $(\hat \theta_n)_ \{n\in\mathbb{N}\}$ such that $\hat \theta_n \overset{P}{\to} \theta_0,$ we want to show the consistency and asymptotic normality of $g_{\hat \theta_n}.$

Why is the asymptotic theory regarding $g_ \{\hat\theta_n\}$ important? As a motivating example, let's consider a binary classification model. For the asymptotics rates, we define small-o and big-o notations in probability as follows.

<div class="definition" text="Landau notation"><br>
$$
    X_n = o_P(a_n) \iff \lim_n P\left(\left| \frac{X_n}{a_n} \right| > \epsilon\right) = 0,~ \forall \epsilon > 0. \\
    X_n = \mathcal{O}_P(a_n) \iff \lim_M\limsup_n P\left(\left| \frac{X_n}{a_n} \right| > M\right) = 0.
    $$
</div> 



In other words, $o_P$ is merely a convergence in probability while $\mathcal{O}_P$ implies stochastic boundedness. That is, 



$$
\hat\theta_n \overset{P}{\to} \theta_0 \iff \hat \theta_n = \theta_0 + o_P(1). \\
\hat \theta_n = E\hat\theta_n + \mathcal{O}_p\left(\sqrt{\text{Var}(\hat\theta_n)}\right).
$$



<br>

## Binary choice model



Suppose we want to predict $Y_i$ (whether the $i$th individual has a job) given information $Z_i$ (education level of the $i$th individual). 

### (case 1) parametric model

Our first model is a paramtric one. Construct a logistic regression model as follows.


$$
Y_i \in \{0, 1\},~ Z_i \in \mathbb R,~ 1\le i\le n.\\
X_i = (Y_i, Z_i)\text{'s are IID.} \\
P(Y=1|Z=z) = F_0(\alpha_0 + \theta_0z), \\
F_0 = \frac{e^x}{1+e^x} \text{ is the CDF of the logistic distribution}.
$$


Further assume that $\alpha_0=0$ so that $\theta_0 \in \mathbb R$ is the only unknown parameter. Our maximum likelihood estimator $\hat \theta_n$  of $\theta_0$ is given as


$$
\hat \theta_n = \argmax_\theta \sum_{i=1}^n \log p_\theta(Y_i|Z_i)
$$


where


$$
p_\theta(y|z) = F_0(\theta_z)^y \{ 1 - F_0(\theta z) \}^{1-y}
$$


is the conditional probability mass of $y$ given $z$.

Define the score function $s_1$ of single observation:


$$
\begin{aligned}
s_1(\theta)
 &= s_1(\theta;y,z) := \frac{d}{d\theta} \log p_\theta(y|z) \\
 &= \frac{d}{d\theta} \left\{ y\log F_0(\theta z) + (1-y)\log (1-F_0(\theta z)) \right\} \\
 &= yz(1-F_0(\theta z)) - (1-y)zF_0(\theta z) \\
 &= z(y-F_0(\theta z)).
\end{aligned}
$$


Define the "Fisher information" as follows.


$$
I_{\theta_0} := Eg_{\theta_0}(Z),
$$


where


$$
g_\theta(z) := \begin{cases}
 -\frac{s_1(\theta)-s_1(\theta_0)}{\theta-\theta_0} = z\cdot\frac{F_0(\theta z) - F_0(\theta_0z)}{\theta-\theta_0},& \text{if } \theta \ne \theta_0 \\
 -\frac{\partial}{\partial\theta_0}s_1(\theta) = z^2F_0(\theta_0z)(1-F_0(\theta_0z)),& \text{if } \theta=\theta_0
\end{cases}
$$


can be regarded as a "second derivative" of $\log p_\theta$ and a "derivative" of $-s_1(\theta)$ evaluated at $\theta_0.$

Our first result gives motivation to some kind of law of large numbers for $g_ \{\hat\theta_n\}$. 

<div class="lemma" text="1.1 implication of extension of LLN">


    $$
    \frac1n \sum_{i=1}^n g_{\hat\theta_n}(Z_i) \overset{P}{\to} I_{\theta_0} > 0
    \implies \sqrt{n}(\hat\theta_n - \theta_0) \overset{d}{\to} \mathcal{N}(0, 1/I_{\theta_0}).
    $$
</div> 

<details>
  <summary>
    expand proof
  </summary>

<div class="proof"><br>
$$
\begin{aligned}
0
 &= \sum_{i=1}^n s_1(\hat\theta_n; Y_i, Z_i) \\
 &= \sum_{i=1}^n s_1(\theta_0) + (\hat\theta_n - \theta_0)\sum_{i=1}^n \frac{s_1(\hat\theta_n) - s_1(\theta_0)}{\hat\theta_n-\theta_0} \\
 &= \sum_{i=1}^n s_1(\theta_0) - (\hat\theta_n-\theta_0)\sum_{i=1}^n g_{\hat\theta_n}(Z_i).
\end{aligned}
$$

Organizing the terms yields 
$$
\begin{aligned}
\sqrt n (\hat\theta_n - \theta_0) 
 &= \sqrt n \cdot \frac{\sum_{i=1}^n s_1(\theta_0;Y_i,Z_i)}{\sum_{i=1}^n g_{\hat\theta_n}(Z_i)} \\
 &=\underbrace{ \left( \frac 1 {\sqrt n} \sum_{i=1}^n s_1(\theta_0) \right) }_{\text{(i)}} / \underbrace{ \left( \frac1n \sum_{i=1}^n g_{\hat\theta_n}(Z_i) \right) }_{\text{(ii)}} 
\end{aligned}
$$
Therefore the result follows from the facts
$$
E_{\theta_0}s_1(\theta_0) = 0,~\text{Var}_{\theta_0}(s_1(\theta_0)) = I_{\theta_0}
$$
and
$$
\text{(i)} \overset d \to \mathcal{N}(0,1), \\
\text{(ii)} \overset P \to I_{\theta_0}.
$$
</div> 

</details>

Since $g_ \{\hat\theta_n\}$ is indexed by $\hat\theta_n$ which is random, to achieve the results above, we need to find a law of large numbers that uniformly bounds all possible $g_\theta,$ $\theta\in\mathbb R.$



Similarly, extension of the central limit theorem can also yield the same result. For this, define 


$$
m(\theta) = m_\theta := E_{\theta_0}s_1(\theta), \\
\sigma^2(\theta) = \sigma_\theta^2 := \text{Var}_{\theta_0}s_1(\theta)
$$


be moments of $s_1(\theta)$ under the true parameter $\theta_0.$ Note that $m(\theta_0)=0,$ $\sigma^2(\theta_0)=I_{\theta_0}$ and by the central limit theorem,


$$
\frac 1 {\sqrt n} \sum_{i=1}^n \big(s_1(\theta)-m(\theta)\big) \overset d \to \mathcal{N}(0, \sigma^2_\theta),~ \forall \theta.
$$


<div class="lemma" text="1.2. implication of extension of CLT">
Suppose $\hat\theta_n = \theta_0 + o_P(1)$ and 
    $$
    \frac 1 {\sqrt n} \sum_{i=1}^n \big(s_1(\hat\theta_n)-m(\hat\theta_n)\big) = \frac 1 {\sqrt n} \sum_{i=1}^n \big(s_1(\theta_0)-m(\theta_0)\big) + o_P(1).
    $$
Then,
    $$
	\sqrt{n}(\hat\theta_n - \theta_0) \overset{d}{\to} \mathcal{N}(0, 1/I_{\theta_0}).
    $$

</div> 

<details>
  <summary>
    expand proof
  </summary>

<div class="proof"><br>
$$
\begin{aligned}
0
 &= \frac 1 {\sqrt n} \sum_{i=1}^n s_1(\hat\theta_n) \\
 &= \frac 1 {\sqrt n} \sum_{i=1}^n \big( s_1(\hat\theta_n) - m(\hat\theta_n) \big) + \sqrt n \cdot m(\hat\theta_n) \\
 &= \frac 1 {\sqrt n} \sum_{i=1}^n \big( s_1(\theta_0) - m(\theta_0) \big) + o_P(1) + \sqrt n \cdot m(\hat\theta_n) \\
 &= \frac 1 {\sqrt n} \sum_{i=1}^n s_1(\theta_0) + o_P(1) + \sqrt n \cdot \big( m(\hat\theta_n) - m(\theta_0) \big) \\
 &= \frac 1 {\sqrt n} \sum_{i=1}^n s_1(\theta_0) + o_P(1) - \sqrt n \cdot (\hat\theta_n - \theta_0)(I_{\theta_0} + o_P(1))
\end{aligned}
$$

The last equality holds since for some $h$ that $h(\hat\theta_n)\overset{P}{\to} 0$ as $\hat\theta_n \overset{P}{\to} \theta_0,$
$$
\begin{aligned}
m(\hat\theta_n)
 &= m(\theta_0) + (m'(\theta_0) + h(\hat\theta_n))(\hat\theta_n - \theta_0) \\
 &= m(\theta_0) - (-I_{\theta_0} + o_P(1))(\hat\theta_n - \theta_0).
\end{aligned}
$$
Organizing the terms gives
$$
\sqrt n (\hat\theta_n - \theta_0) = \left( \frac 1 {\sqrt n} \sum_{i=1}^n s_1(\theta_0) + o_P(1) \right) / \left( I_{\theta_0} + o_P(1) \right) \overset d \to \mathcal{N}(0, 1/I_{\theta_0}).
$$
</div> </details>

<br>



### (case 2) nonparametric isotonic model

The model assumption that the conditional probability follows logistic distribution is quite strong. Instead, we will impose as few assumptions as possible and construct a nonparametric model.

The only assumption that we will impose is that $F_0$ is a monotonically increasing function that is bounded between 0 and 1. i.e. the parameter space is


$$
F_0 \in \Lambda := \{F: \mathbb R \to [0,1],~ F \text{ is increasing}\}.
$$


The MLE can be found similarly as in the case 1:


$$
\hat F_n = \argmax_{F \in \Lambda} \sum_{i=1}^n \big( Y_i \log F(Z_i) + (1-Y_i)\log (1-F(Z_i)) \big).
$$


Suppose $Z_i \sim Q,$ then the $L^2(Q)$-distance between the MLE and $F_0$ can be shown as


$$
\begin{aligned}
\|F_n - F_0\|_{2, Q}
 &= \left\{ \int\big( \hat F_n - F_0 \big)^2 dQ \right\}^{1/2} \\
 &= \mathcal{O}_P(n^{-1/3})
\end{aligned}
$$


One can also show that the same rate holds for the Hellinger distance as well.

<br>

### (case 3) nonparametric concave model

In addition to the second model, we can restrict the shape of the function further by adding concavity constaint. To be specific, assume that


$$
F_0 \in \tilde\Lambda := \{F:\mathbb R \to [0,1],~ 0\le\frac{dF}{dz}\le M,~ F \text{ is concave} \}.
$$


The derivative condition implies that $F$ is increasing no faster than the rate of $M.$ It can be shown later that this model has slightly improved rate of $L^2(Q)$-convergence of $\mathcal{O}_P(n^{-2/5}).$



<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).



<br>

[^2]: Billingsley, 1999, *Convergence of Probability Measures*, 2nd edition.
