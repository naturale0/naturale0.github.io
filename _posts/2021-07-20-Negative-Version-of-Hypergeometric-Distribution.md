---
layout: post
title: "Negative Version of Hypergeometric Distribution"
date:   2021-07-20 19:59:00 +0900
author: "Sihyung Park"
categories: [probability]
---



It is a well known and popular fact that the number $X$ of i.i.d. Bernoulli trials, with success probability $p,$ until the fixed $r$-th success follows the distribution with probability mass function given as


$$
\mathbb P(X=x) = {x-1 \choose r-1} p^r (1-p)^{x-r},~ x\ge r
$$


As can be seen, mass of $X$ resembles that of binomial distribution. The difference comes from the fact that instead of fixing the total number of trials $n$ as in binomial distribution, distribution of $X$ fixes the number of success $r.$ From this relationship, we name such distribution the *negative binomial* distribution $\text{NB}(r,p).$

While the negative binomial random variables are popular, I haven't seen the without-replacement counterpart until 2019, namely, the **negative hypergeometric** distribution. From its name and the fact that the with-replacement counterpart of the binomial distribution is the hypergeometric distribution, we can infer relationship between negative hypergeometric and hypergeometric distribution.

<br>

## Negative hypergeometric distribution

Suppose we have an urn with $N$ total balls in it. Among those, $K$ balls are colored black and the remainings are colored white. We regard drawing a black ball as a success event. We will draw balls <u>without</u> replacement. 

Let $X$ be the number of trials until the pre-specified number of $r$-th black ball is drawn. Then the probability of $X=x$ is the product of two probabilities: First being the one that is from drawing $(r-1)$ black balls without replacement, and the second being the one from drawing the last $r$-th black ball.


$$
\begin{aligned}
\mathbb P(X=x)
 &= \frac{ {K \choose r-1}{N-K \choose x-r} } {N \choose x-1} \cdot \frac{K-(r-1)}{N-(x-1)} \\
 &= \frac{\color{darkgreen}{ K! } }{\color{darkred}{(r-1)!} \color{darkblue}{(K-r)!} } \frac{\color{darkgreen}{ (N-K)! } }{\color{darkred}{(x-r)!} \color{darkblue}{(K-r)!} } \bigg/ \frac{\color{darkgreen}{ N! } }{\color{darkred}{(x-1)!} \color{darkblue}{(N-x)!} } \\
 &= \frac{\color{darkblue}{N-x \choose K-r} \color{darkred}{x-1 \choose r-1} }{\color{darkgreen}{N \choose K} },~ r \le x \le N-K+r
\end{aligned} \tag{1}\label{pmf}
$$



We name the distribution of such $X$ by negative hypergeometric distribution $\text{NH}(x;N,K,r).$

Note that surprisingly, organizing the terms results in the denominator that is independent to the value of $x.$ This formulation allows us to compute moments easily.

<br>

## Moments

To compute moments, we need two lemmas.

<div class="lemma" text="binomial identity">


$$
{n \choose k} = (-1)^k{k-n-1 \choose k}
$$
</div> 



<div class="lemma" text="Chu-Vandermonde">

$$
\sum_{k=0}^c{a \choose k}{b \choose c-k } = {a+b \choose c}
$$

</div> 



Since the solution for higher order moments is inductive, I will only present computation of expectation.


$$
\begin{aligned}
\mathbb EX 
 &= \sum_{x=r}^{N-K+r} x \frac{ {N-x \choose K-r} {x-1 \choose r-1} }{N \choose K} \\
 &= \sum_{k=0}^{N-K} (k+r) \frac{ {N-r-k \choose N-K-k} {k+r-1 \choose k} }{ {N \choose K} } \\
 &= \frac{r}{N \choose K} \sum_{k=0}^{N-K} {N-r-k \choose N-K-k}{k+r \choose k}
\end{aligned}
$$


Apply lemma 1 so that


$$
{k+r \choose k} = (-1)^k {-r-1 \choose k}, \\
{N-r-k \choose N-K-k} = (-1)^{N-K-k} {r-K-1 \choose N-K-k}.
$$


Now apply lemma 2 and lemma 1 again then the expectation becomes


$$
\begin{aligned}
\mathbb EX
 &= \frac{r}{N \choose K} (-1)^{N-K} \sum_{k=0}^{N-K} {r-K-1 \choose N-K-k}{-r-1 \choose k} \\
 &= \frac{r}{N \choose K} (-1)^{N-K} {-K-2 \choose N-K} \\
 &= \frac{r}{N \choose K} {N+1 \choose N-K} \\
 &= r\cdot\frac{N+1}{K+1}.
\end{aligned}
$$


In fact, the same technique can be used to prove that $\eqref{pmf}$ is a legit probability mass function.

