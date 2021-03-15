---
layout: post
title: "[Statistical Learning] 2. Linear classifiers"
date:   2021-03-16 00:44:00 +0900
author: "Sihyung Park"
categories: [statistical learning]
---



In this chapter, linear classifiers will be introduced and will be compared. Specifically, logistic regression and linear discriminant analysis will be described in detail.



- TOC
{:toc}
<br> 

## Linear classifiers

Here, our setting will be binary classification problem. That is,


$$
\mathcal{Y}=\{0,1\} \text{ or } \{-1,1\},\\
\ell(y,a) = \mathbf{1}(y\ne a).
$$


Linear model assumes linear decision boundary:


$$
\{x: \beta_0 + x'\boldsymbol{\beta} = 0\}.
$$


Under this decision boundary, our classifier $G: \mathbb{R}^p \to \mathcal{Y}$ will be


$$
G(x) = \text{sign}\big(f(x)\big),~ f(x)=\beta_0 + x'\boldsymbol{\beta}.
$$


<br>

### Descriptive vs. generative model

Descriptive model models $\mathbb{P}(y\|x),$ while generative model models both $\mathbb{P}(x\|y)$ and $\pi(y)$ which makes it possible to model the joint probability $\pi(x,y).$ While descriptive model generally requires less assumptions and performs better, generative model can "generate" the data according to modeled joint probability, thus more explainable.

<br>



## Linear discriminant analysis

Linear discriminant analysis, or LDA, is a generative approach to classification. It assumes the density of $x$ given $y=j$ to be that of normal distribution. i.e.


$$
f_j(x) = \mathbb{P}(x|y=j) := \phi_{(\mu_j, \Sigma_j)}(x),
$$


where $\phi_{(\mu, \Sigma)}$ is the density of $\mathcal{N}(\mu, \Sigma).$ Bayes classifier can be easily achieved as


$$
\begin{aligned}
G(x)
 &:= \text{sign}\left( \log\frac{\mathbb{P}(y=1|x)}{\mathbb{P}(y=-1|x)} \right) \\
 &= \text{sign} \big( \delta_1(x) - \delta_{-1}(x) \big)
\end{aligned}
$$


where


$$
\begin{aligned}
\delta_j(x)
 &= \log \mathbb{P}(y=j|x) \\
 &= \log \mathbb{P}(x|y=j) + \log \pi_j \\
 &= -\frac{1}{2}\log|\Sigma_j| -\frac{1}{2}(x-\mu_j)^\intercal \Sigma_j^{-1}(x-\mu_j) + \log\pi_j + C
\end{aligned}
$$


is the discriminant function. If we assume that $\Sigma_1 = \Sigma_{-1} = \Sigma,$ then the discriminant function can be represented as linear function with respect to $x$ as the quadratic terms are cancelled out:


$$
\delta_j(x) = \mu_j^\intercal\Sigma^{-1}x - \frac{1}{2}\mu_j^\intercal \Sigma^{-1} \mu_j + \log\pi_j.
$$


In practice, we use sample version of parameters instead:

* $\hat \mu_j = \frac{1}{n_j} \sum_{i=1}^n x_i \mathbf{1}(y_i=j)$
* $\hat \Sigma_j = \frac{1}{n_j-1}(x_i - \hat \mu_j)(x_i - \hat \mu_j)^\intercal$
* $n_j = \sum_{i=1}^n \mathbf{1}(y_i=j)$
* $\pi_j = n_j/n$
* $\hat\Sigma = \frac{1}{n-2}\bigr\{ (n_1-1)\hat\Sigma_1 + (n_{-1}-1)\hat\Sigma_{-1} \bigr\}$

<br>



## Logistic regression

Logistic regression is a descriptive model that models log odds as a linear function. It starts from the decision boundary of the data with $\mathcal{Y} = \{0, 1\}.$ We want to classify the data by the decision boundary


$$
\begin{aligned}
&\{x: \mathbb{P}(Y=1|X=x) = 0.5\} \\
&= \left\{x: \frac{\mathbb{P}(Y=1|X=x)}{\mathbb{P}(Y=0|X=x)} = 1\right\} \\
&= \left\{x: \log\frac{\mathbb{P}(Y=1|X=x)}{\mathbb{P}(Y=0|X=x)} = 0\right\}.
\end{aligned}
$$


The simplest way is to let the LHS to be a linear function.


$$
\log\frac{\mathbb{P}(Y=1|X=x)}{\mathbb{P}(Y=0|X=x)} \overset{\text{set}}{=} x^\intercal\boldsymbol{\beta}.
$$


Organizing both sides yields


$$
\mathbb{P}(Y=1|X=x) = \frac{e^{x^\intercal\boldsymbol{\beta}}}{1+e^{x^\intercal\boldsymbol{\beta}}} =: \phi(x,\boldsymbol\beta)
$$


which is the logistic regression model. To estimate the best $\boldsymbol\beta,$ we use maximum likelihood estimator of it. The log likelihood $\ell$ is


$$
\begin{aligned}
\ell(\boldsymbol{\beta})
 &= \sum_{i=1}^n \log \mathbb{P}(Y=y_i|X=x_i) \\
 &= \sum_{i=1}^n \bigg[ y_i\log\mathbb{P}(Y=1|X=x_i) + (1-y_i)\log\mathbb{P}(Y=0|X=x_i) \bigg] \\
 &= \sum_{i=1}^n \bigg[ y_i\log\frac{\mathbb{P}(Y=1|X=x_i)}{\mathbb{P}(Y=0|X=x_i)} + \log\mathbb{P}(Y=0|X=x_i) \bigg] \\
 &= \sum_{i=1}^n \big[ y_i\cdot x_i^\intercal\boldsymbol{\beta} - \log(1+x_i^\intercal\boldsymbol{\beta}) \big].
\end{aligned}
$$


Since it cannot be directly maximized, we use Newton-Raphson method:


$$
\boldsymbol{\beta}^{(t+1)} = \boldsymbol{\beta}^{(t)} - \left( \frac{\partial^2\ell}{\partial\boldsymbol{\beta}^{(t)} \partial\boldsymbol{\beta}^{(t)\intercal}} \right)^{-1} \frac{\partial\ell}{\partial \boldsymbol{\beta}^{(t)}}
$$


or iteratively reweighted least squares (IRLS), which is actually equivalent to Newton method:


$$
\begin{aligned}
\boldsymbol{\beta}^{(t+1)} 
 &= (X^\intercal W^{(t)}X)^{-1} (X^\intercal W^{(t)} Z^{(t)}) \\
 &= \argmax_\boldsymbol{\beta} (Z^{(t)} -X\boldsymbol{\beta}^{(t)})^\intercal W^{(t)} (Z^{(t)} - X\boldsymbol{\beta}^{(t)})
\end{aligned}
$$


where


$$
W^{(t)}_{(i,i)} = \phi(x_i, \boldsymbol{\beta}^{(t)}) (1 - \phi(x_i, \boldsymbol{\beta}^{(t)})), \\
Z^{(t)} = X\boldsymbol{\beta}^{(t)} + W^{-1}(y-p^{(t)}), \\
p^{(t)} = \big[ \phi(x_i, \boldsymbol{\beta}^{(t)}) \big]_{i=1}^n.
$$


<br>



## LDA vs. Logistic regression

[TBD]













<br>



***References***

* Hastie, Tibshirani, Friedman. 2008. **The Elements of Statistical Learning**. 2nd edition. Springer.
* **Advanced Data Mining (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Yongdai Kim).