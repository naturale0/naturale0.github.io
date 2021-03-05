---
layout: post
title: "[Statistical Learning] 1. Overview of Supervised Learning"
date:   2021-03-03 00:13:00 +0900
author: "Sihyung Park"
categories: [statistical learning]

---

The `[Statistical Learning]` series of posts are my summary of *The Elements of Statistical Learning* (ESL) and a memo on the lecture *Advanced Data Mining (Spring, 2021)* by Prof. Yongdai Kim. Main goal of the lecture is to interpret classical machine learning models in terms of statistics and decision theoretic framework.

The first chapter (actually the second in ESL) is an overview of supervised learning, especially the two extremes - linear regression and k-nearest neighbor - their weakness and methods to overcome those.

- TOC
{:toc}
<br>




## Notations

* $\mathbf{X} \in \mathbb{R}^p$ is the covariate (input).
* $Y \in \mathcal{Y}$ is the response (output).

We assume $(Y,\mathbf{X}) \sim P$ for unknown distribution $P$. If $\mathcal{Y}=\mathbb{R}$, then the problem to solve becomes a regression one. If $\mathcal{Y}=\{0,1\}$, the problem is now a binary classification.

* $\phi$ is the true relationship (system) between $X$ and $Y$.

That is, $Y=\phi(X,\epsilon)$ is the true model with error $\epsilon$ that is intrinsic to the system. Our goal is to find a model that best approximates $\phi$. In order to do so,

* Set a loss function $\ell(y,a)$.
* Set a family of functions $\mathcal{F}$.

Under this setting, our best approximation to $\phi$ would be


$$
f^0 := \argmin_{f\in\mathcal{F}} E_{\mathbf{X},Y} \ell(Y, f\left(\mathbf{X})\right).
$$


The minimand in the right hand side is called the *expected prediction error (EPE)*. In other words, $f^0 := \arg\min_{f\in\mathcal{F}} \text{EPE}(f).$

Unfortunately, we cannot compute $E_{\mathbf{X},Y}$ since $P$ is unknown. We need to further approximate $f^0$ by $\hat f$, using the observed data


$$
\mathcal{L} := \{(y_i, \mathbf{x}_i): (y_i, \mathbf{x}_i) \overset{\text{iid}}{\sim} P,~ i=1,\cdots,n\},
$$


which we denote the training data. With the help of $\mathcal{L}$, our model finally becomes $\hat f(\mathbf{x}) = f(\mathbf{x},\mathcal{L}).$ With this model, we can predict the unknown response $y^\*$ associated with new input $\mathbf{x}^\*$ with $\hat f(\mathbf{x}^*).$

<br>



## Linear regression vs. k-nearest neighbor

In this section, linear model and k-NN will be compared in uncomplicated regression and classification problems.

### Regression problem

In this regression setting, $\ell(y, a) = (y-a)^2$ would be the loss and $\text{EPE}(f) = E_{\mathbf{X},Y} \left(Y - f(\mathbf{X})\right)^2$ is to be minimized.

From all possible functions, our best choice will be


$$
f^0 = \argmin_{f} \text{EPE}(f) = E(Y|X).
$$


This can be easily proved by conditioning the EPE as follows:


$$
\begin{aligned}
E_{\mathbf{X},Y} \left(Y - f(\mathbf{X})\right)^2 = E_{\mathbf{X}} E_{Y|\mathbf{X}} \left( \left(Y-f(\mathbf{X})\right)^2 \vert \mathbf{X}) \right)
\end{aligned}.
$$


We call this the regression function. Linear regression and k-NN both approximate $f^0$, but in different ways.

<br>

#### OLS regression

Assume that the model is in fact quite linear:


$$
f^0(\mathbf{x}) \approx \beta^0_0 + \sum_{k=1}^p x_k\beta^0_k.
$$


We start by constraining the model by setting a family of linear functions.


$$
\mathcal{F}=\left\{\beta_0 + \sum_{k=1}^p x_k \beta_k : \beta_k \in \mathbb{R}, i=1,\cdots,p\right\}.​
$$


As we can see, any function in $\mathcal{F}$ is characterized by corresponding values of $\mathbf{\beta}$. In other words, $f \in \mathcal{F}$ is **parametrized** by parameters $\mathbf{\beta}.$ Thus the process of finding $\hat f$ that approximates $f^0$ becomes the process of finding $\hat{\mathbf{\beta}}$ that approximates $\mathbf{\beta}^0$. In this setting and perspective,


$$
\text{EPE}(f) = E(Y-\mathbf{X}\beta)^\intercal(Y-\mathbf{X}\beta)
$$


Hence,


$$
\beta^0 = [E(XX^\intercal)]^{-1} E(XY).
$$


Hence OLS estimator $\hat\beta$ can be interpreted as a method-of-moment (MOM) estimator for $\beta^0.$


$$
\hat\beta = \left( \frac{1}{n} \sum_{i=1}^n \mathbf{x}_i\mathbf{x}_i^\intercal \right) \left( \frac{1}{n} \sum_{i=1}^n \mathbf{x}_i y_i \right).
$$


<br>

#### k-nearest neighbor

On the other hand, k-NN starts by defining *k-nearest neighbors of $x$*


$$
N_k(\mathbf{x}) := \{i: \mathbf{x}_i \text{ are the $k$ closest points of $\mathbf{x}$, } (y_i, \mathbf{x_i})\in \mathcal{L}\}.
$$


This can be seen as an approximaton of conditionality $(\cdot \vert \mathbf{X}=\mathbf{x})$. By averaging responses associated with training data in $N_k(\mathbf{x})$, k-NN model can also be regarded as a MOM estimator.


$$
\hat f (\mathbf{x}) = \frac{1}{k} \sum_{i \in N_k(\mathbf{x})} y_i = \text{Average}\left(y_i \vert i \in N_k(\mathbf{x})\right).
$$


It is known that $\hat f(\mathbf{x}) \to f^0 (\mathbf{x})$ for all $\mathbf{x} \in \mathbb{R}^p$ as $n,k\to\infty$ and $\frac{k}{n} \to 0.$ Note that since the complexity of the model becomes higher as the tuning paramter $k$ grows (in fact the complexity is inversely proportionate to $k$). So the $\frac{k}{n}\to0$ part tells us to adjust $k$ to be small relative to $n.$

Unlike OLS, k-NN model cannot be represented analytically. Such model is sometimes referred to as a data model. Also note that the model function is not parametrized.

<br>

#### OLS again, as empirical risk minimization.

Until now, the general process was:

1. Find $f^0 = \arg\min_f \text{EPE}(f).$
2. Approximate $f^0$ with $\hat f$.

From here on throughout the lecture, we would like to interpret each model as a result of **empirical risk minimization**:

1. Approximate the EPE with an *empirical risk*.
2. Find $\hat f = \arg\min_f (\text{empirical risk of $f$}).$

For example, by setting an empricial risk of $f$ as


$$
\frac{1}{n} \sum_{i=1}^n \left(y_i - f(\mathbf{x_i})\right)^2,
$$


OLS regression can be seen as an empricial risk minimizer since 


$$
\hat \beta = \argmin_\beta \frac{1}{n} \sum_{i=1}^n \left(y_i - f(\mathbf{x_i})\right)^2.
$$


In this interpretation, we hope that for large enough $n$'s, $\hat \beta$ would also be the minimizer of EPE. However, we need uniform convergence $g_n \to g$ to ensure convergence of $\arg\min_x g_n(x) \to \arg\min_xg(x).$ This will not be covered in this lecture.

<br>



### Classification problem

Here, we consider a classification problem with $J$ possible classes. That is, $\mathcal{Y} = \{1,\cdots,J\}.$ Expected predictive error becomes


$$
\begin{aligned}
\text{EPE}(f) &= E_{\mathbf{X},Y} \ell(Y, f(\mathbf{X})) \\
  &= E_\mathbf{X} E_{Y\vert\mathbf{X}} \left( \ell\left(Y, f(\mathbf{X}) \vert \mathbf{X}\right) \right) \\
  &= E_\mathbf{X} \sum_{j=1}^J \ell(j, f\left(\mathbf{X})\right) P(Y=j \vert \mathbf{X}).
\end{aligned}
$$


Thus by pointwisely minimizing it we get the minimizer


$$
f^0(x) = \argmin_{k=1,\cdots,J} \sum_{j=1}^J \ell(j, f(\mathbf{x})) P(Y=j|\mathbf{X}=\mathbf{x}).
$$


If we set the 0-1 loss $\ell(y,a) = \mathbf{1}(y \ne a)$ as the loss function,


$$
\begin{aligned}
f^0(\mathbf{x})
  &= \argmin_{k=1,\cdots,J} P(Y\ne k | \mathbf{X}=\mathbf{x}) \\
  &= \argmax_{k=1,\cdots,J} P(Y=k|\mathbf{X} = \mathbf{x}).
\end{aligned}
$$


becomes the optimal classifier. This is very intuitive since we select the class that maximizes the (posterior) probability given observed data. This form of classifier is called a **Bayes classifier (Bayers rule)**, and the EPE of Bayes classifier is called the **Bayes risk**.

There are several remarks on Bayes risk:

1. No other classifier better performs that Bayes classifier.
2. Bayes risk is not zero.

Thus even if we have as many data as we want, we cannot lower the error smaller than the Bayes risk.

3. Bayes risk is unknown and need to be guessed.

Estimation of the Bayes risk is done by approximating the probability $\phi_j(\mathbf{x}) := P(Y=k\|\mathbf{X}=\mathbf{x}).$

**k-nearest neighbor** approximates it as an empirical probability


$$
\hat \phi_k (\mathbf{x}) = \frac{1}{k} \sum_{i\in N_k(\mathbf{x}) \mathbf{1}} (y_i=j).
$$


Although OLS regression is not suitable since it does not guarantee the values in $[0, 1],$ **logistic regression** can be used to approximate $\phi_j$.



<br>



***References***

* Hastie, Tibshirani, Friedman. 2008. **The Elements of Statistical Learning**. 2nd edition. Springer.
* **Advanced Data Mining (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Yongdai Kim).
