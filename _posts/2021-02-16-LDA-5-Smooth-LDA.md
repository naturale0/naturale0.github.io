---
layout: post
title: "Understanding Latent Dirichlet Allocation (5) Smooth LDA"
date:   2021-02-17 00:51:00 +0900
author: "Sihyung Park"
categories: [bayesian, machine learning, natural language processing]

---

From background to two inference processes, I covered all the important details of LDA so far. One thing left over is a difference between (basic) LDA and *smooth LDA*. Consider this last post as a cherry on top.

> ***This article is the fifth and the final part of the series "Understanding Latent Dirichlet Allocation".***
>
> 1. [Backgrounds](/natural%20language%20processing/LDA-1-background-topic-modelling)
> 2. [Model architecture](/bayesian/machine%20learning/natural%20language%20processing/LDA-2-The-Model)
> 3. [inference - variational EM](/bayesian/machine%20learning/natural%20language%20processing/LDA-3-Variational-EM)
> 4. [inference - Gibbs sampling](/bayesian/machine%20learning/natural%20language%20processing/LDA-4-Gibbs-Sampling)
> 5. smooth LDA



- TOC
{:toc}
<br> 

## Empirical vs. fuller Bayes

Not every Bayesian approches are the same. One of the most important aspect when applying Bayesian model to real-world data is decision of hyperparameters. For the task, empirical Bayes method "fit" the model to the data to derive, in many times, *point estimate* of hyperparameter, while standard (fuller) Bayes predefine the *prior distribution* before any data and update it later using the data as an evidence.

Recall the basic LDA that I explained from [the first](/natural%20language%20processing/LDA-1-background-topic-modelling) to [the third](/bayesian/machine%20learning/natural%20language%20processing/LDA-3-Variational-EM) articles. Pay attention to the part that hyperparameter $\beta$ does not have a distribution; it is assumed to be an unknown but *fixed* value. This makes the basic LDA an empirical Bayes model. Can we extend this to make a fuller Bayes model?



<br>

## Smooth LDA

In order to extend the model to be fully Bayesian, all we need to do is to regard $\beta$ as another hidden parameter by adding a Dirichlet prior $\beta \sim \mathcal{D}(\lambda)$ to it. Blei et al. (2003) provides a graphical representation of this extended, or **smoothed** version of LDA. I added a modified variational distribution for it next to the figure.



![210216_smooth-lda-vem](/assets/fig/210216_smooth-lda-vem.png)



So why would we want to make a model fully Bayesian? This is because of generability. If we use fixed point estimate for $\beta$, we get word-topic assignment that assigns probability zero to words that were not in training data. By giving $\beta$ a distribution, we can smooth it out to assign positive probability to all known and unknown words. In this perspective, it can be seen as a smoothing method.



<br>

## Variational EM for smooth LDA

I already explained inference methods for smooth LDA: [Gibbs sampling with Metropolis-Hastings rule](/bayesian/machine%20learning/natural%20language%20processing/LDA-4-Gibbs-Sampling#gibbs-sampling) proposed by Pritchard et al. (2000), and [Collapsed gibbs sampling](/bayesian/machine%20learning/natural%20language%20processing/LDA-4-Gibbs-Sampling#collapsed-gibbs-sampling) that Griffiths and Steyvers (2002) proposed are the ones. Here I would like to continue the discussion and be more specific on variational EM method that Blei et al. (2003) presented. If you are not familiar with variational EM algorithm, please take a look into the previous articles before moving on.

<br>

### E-step

As in the figure that I put next to the Figure 7, we add additional variational parameter $\eta$ that acts as a surrogate of $\lambda$ and consider $\beta_i \sim \mathcal{D}_V(\lambda)$ for all $i=1,\cdots,k$ by exchangeability. Then the variational distribution becomes


$$
q(\theta, \mathbf{z}, \beta|\gamma,\phi,\lambda) = \prod_{i=1}^k \mathcal{D}_V(\beta_i|\lambda_i) \prod_{d=1}^M q\big(\theta_d, \mathbf{z}_d|\gamma(\mathbf{w}_d),\phi(\mathbf{w}_d)\big)
$$


Since $\beta$ part is multiplicative to the others, update rule for $\phi$ and $\gamma$ remains the same. (Actually, update rule of $\phi$ changes a little as it contained a term $\beta$ which is now considered a random variable.) Update rule for $\lambda$ is easy to derive by (again) differentiating the variational lower bound $L$.

There were no derivation depicted in the Blei et al. (2003), so I did one by myself. The variational lower bound $L$ is


$$
\begin{aligned}
L(\gamma,\phi,\lambda | \alpha,\eta)
  &= M\sum_{i=1}^k \biggr( \log\Gamma\biggr(\sum_{j=1}^V\eta_j\biggr) - \sum_{j=1}^V\log\Gamma(\eta_j) + \sum_{j=1}^V (\eta_j\cancel{-1})\big(\Psi(\lambda_i) - \Psi(V\lambda_i)\big) \biggr) \\
  &+ \sum_{d=1}^M\left(\log\Gamma\biggr(\sum_{i=1}^k\alpha_i\biggr) - \sum_{i=1}^k \log\Gamma(\alpha_i) + \sum_{i=1}^k(\alpha_i-1)\left( \Psi(\gamma_{di}) - \Psi\biggr(\sum_{i=1}^k \gamma_{di}\biggr) \right)\right) \\
  &+ \sum_{d=1}^M\sum_{n=1}^{N_d}\sum_{i=1}^k \phi_{dni}\left(\Psi(\gamma_{di}) - \Psi\biggr(\sum_{i=1}^k \gamma_{di}\biggr)\right) \\
  &+ \sum_{d=1}^M\sum_{n=1}^{N_d}\sum_{i=1}^k\sum_{j=1}^V \phi_{dni}w_{dn}^j\big( \Psi(\lambda_i) - \Psi(V\lambda_i) \big) \\
  &- M\sum_{i=1}^k \biggr( \log\Gamma(V\lambda_i) - V\log\Gamma(\lambda_i) + V(\lambda_i\cancel{-1})\big( \Psi(\lambda_i)-\Psi(V\lambda_i) \big) \biggr) \\
  &- \sum_{d=1}^M \left( \log\Gamma\biggr(\sum_{i=1}^k \gamma_{di}\biggr) - \sum_{i=1}^k \log\Gamma(\gamma_{di}) + \sum_{i=1}^k(\gamma_{di}-1)\biggr(\Psi(\gamma_{di}) - \Psi\biggr(\sum_{i=1}^k \gamma_{di}\biggr)\biggr) \right)  \\
  &- \sum_{d=1}^M\sum_{n=1}^{N_d}\sum_{i=1}^k \phi_{dni}\log\phi_{dni}  .
\end{aligned}
$$


Organize only the terms with $\lambda$ and differentiate it then we get


$$
\begin{aligned}
\frac{\partial L}{\partial \lambda_i}
  = &- \Psi'\left(V \lambda_{i}\right) + V \Psi'\left(\lambda_{i}\right) \\
    &- \cancel{V \big( \Psi'(\lambda_{i}) - \Psi'\left( V \lambda_{i} \right) \big)} \\
    &- V (\lambda_{i}\cancel{-1})\big(\Psi'(\lambda_{i}) - \Psi'\left(V \lambda_{i}\right)\big) \\
    &+ \sum_{n=1}^{N_d}\sum_{j=1}^V \phi_{dni} w_{dn}^j \big( \Psi'(\lambda_i) - \Psi'(V\lambda_i) \big) \\
    &+ \sum_{j=1}^V(\eta_j-1)\big( \Psi'(\lambda_i) - \Psi'(V\lambda_i) \big)
\end{aligned}
$$



Thus letting it zero yields the update rule for $\lambda$:



$$
\lambda_i^{(t+1)} = \eta^{(t)} + \sum_{d=1}^M\sum_{n=1}^{N_d} \phi_{dni}^{(t)}w_{dn}^j.
$$



<br>

### M-step

Update rule for $\alpha$ is the same: we update it using linear-time Newton-Raphson. What is important is that update rule for $\eta$ is also the same as $\alpha$. It can be confirmed by organizing only the terms with $\eta$.


$$
L_{[\eta]} = \sum_{i=1}^k \left( \log\Gamma\biggr(\sum_{j=1}^V \eta_j\biggr) - \sum_{j=1}^V\log\Gamma(\eta_j) + \sum_{j=1}^V (\eta_j-1)\biggr( \Psi(\lambda_{ij}) - \Psi\biggr(\sum_{j=1}^V\lambda_{ij}\biggr) \biggr) \right).
$$


This is exactly the same as $L_{[\alpha]}$ if replacing $\eta$ with $\alpha$, $k$ with $M$, and $\eta$ with $\gamma$. Thus by exactly the same algorithm, we can update $\eta$.

To summarize, the **whole process of variational EM is as follows**: First, initialize $\phi_{dni}^{(0)} := 1/k$ for all $i=1,\cdots,k$ and $n=1,\cdots,N_d$ along with $\gamma_{di}^{(0)} := \alpha_i^{(0)} + N/k$ for all $i=1,\cdots,k$. Then repeat the following until convergence.

3. In the E-step, for $d=1,\cdots,M$,
    1. For $n=1$ to $N$ and $i=1$ to $k$,
        1. $\phi_{dni}^{(t+1)} = \exp\left(\Psi(\lambda_i^{(t)} - \Psi\big(V \lambda_{i}^{(t)}\big) + \Psi(\gamma_{di}^{(t)} - \Psi\big(\sum_{j=1}^k \gamma_{dj}^{(t)}\big)\right)$.
        2. For $j=1, \cdots, V$,
            1. $\lambda_{ij}^{(t+1)} = \eta + \sum_{d=1}^M \sum_{n=1}^{N_d} \phi_{dni}^{(t+1)} w_{dn}^j$.
    2. Normalize $\phi_{dn}^{(t+1)}$ to sum to 1.
    3. $\gamma_d^{(t+1)} = \alpha + \sum_{n=1}^N \phi_{dn}^{(t+1)}$.
2. In the M-step,
    1. Update $\alpha^{(t+1)}$ with linear-time Newton-Raphson.
    2. Update $\eta^{(t+1)}$ with linear-time Newton-Raphson.

<br>

*Python code for the algorithm is in the last part of [this notebook (GitHub)](https://github.com/naturale0/NLP-Do-It-Yourself/blob/main/NLP_with_PyTorch/3_document-embedding/3-1.%20latent%20dirichlet%20allocation.ipynb).*



<br>



***References***

* Blei, Ng, Jordan. 2003. **Latent Dirichlet Allocation**. Journal of Machine Learning Research. 3 (4–5): 993–1022.