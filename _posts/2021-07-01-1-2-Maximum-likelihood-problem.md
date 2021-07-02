---
layout: post
title: "1.2. Mean Estimation in the Binary Choice Problem"
date:   2021-07-01 00:23:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



Another motivating example can be found in the estimation of mean of the binary choice model.

- TOC
{:toc}
<br> 

## Mean estimation in the binary classification

Our model is from the [(case 2) of the previous article](/empirical%20process/asymptotics/empirical%20processes%20in%20m-estimation/1-1-Motivating-example#case-2-nonparametric-isotonic-model).


$$
P(Y=1|Z=z) = F_0(z),~ Z\sim Q,~ F_0\in\Lambda, \\
\Lambda := \{F:\mathbb R \to [0,1],~ F \text{ is increasing}\}.
$$


This time the estimand is the population mean


$$
\begin{aligned}
\theta_0=\theta_{F_0}
 &:=\int F_0(z) dQ(z) = E F_0(Z) \\
 &= P(Y=1) = EY.
\end{aligned}
$$


By definition, it is clear that $E\big[ Y_i - F_0(Z_i) \big] = 0.$

We will only consider the case where $Q$ is known. In this case, the MLE of $F_0$ becomes


$$
\hat\theta_n = \theta_{\hat F_n} = \int \hat F_n(z) dQ(z),
$$


where $\hat F_n$ is the MLE of $F_0.$ 

For $F \in \Lambda,$ define


$$
\theta_F = \int F(z) dQ(z),
$$


then by the classical central limit theorem, we get


$$
\frac 1 {\sqrt n} \sum_{i=1}^n \big( F(Z_i) - \theta_F \big) \overset d \to \mathcal{N}(0, \text{Var}(F(Z))).
$$


Again, if we prove some form of functional CLT for all $F\in\Lambda,$ then together with the result form the classical CLT, we get the asymptotic distribution of the MLE.



<div class="lemma" text="1.4">
$$
    \frac 1 {\sqrt n} \sum_{i=1}^n \big( \hat F_n(Z_i) - \hat\theta_n \big) = \frac 1 {\sqrt n} \sum_{i=1}^n \big( F_0(Z_i) - \theta_0 \big) + o_P(1) \\
    \implies \sqrt n (\hat\theta_n - \theta_0) \overset d \to \mathcal{N}\left( 0, \int F_0(z)(1-F_0(z)) dQ(z) \right).
$$
</div> 

   <div class="proof"><br>
We will take the fact $\frac1n \sum_{i=1}^n \hat F_n(Z_i)=\bar Y$ for granted. By this fact,
$$
\begin{aligned}
\sqrt n (\hat\theta_n - \theta_0)
 &= \sqrt n (\bar Y - \theta_0) - \sqrt n (\bar Y - \hat\theta_n) \\
 &= \sqrt n (\bar Y - \theta_0) - \frac 1 {\sqrt n} \sum_{i=1}^n \big( \hat F_n(Z_i) - \hat\theta_n \big) \\
 &= \sqrt n (\bar Y - \theta_0) - \frac 1 {\sqrt n} \sum_{i=1}^n \big( F_0(Z_i) - \theta_0 \big) + o_P(1) \\
 &= \frac 1 {\sqrt n} \sum_{i=1}^n \big( Y_i - \cancel{\theta_0} - F_0(Z_i)  + \cancel{\theta_0} \big) + o_P(1).
\end{aligned}
$$
By the classical CLT,
$$
\begin{aligned}
\frac 1 {\sqrt n} \sum_{i=1}^n \big( Y_i - F_0(Z_i) \big) \overset d \to \mathcal{N}\left( 0, \text{Var}(Y-F_0(Z)) \right).
\end{aligned}
$$
The variance can be rewritten as
$$
\begin{aligned}
\text{Var}(Y-F_0(Z))
 &= E[Y-F_0(Z)]^2 \\
 &= E[Y^2 - 2YF_0(Z) + F_0^2(Z)] \\
 &= E[Y^2 - F_0^2(Z)] \\
 &= EY - EF_0^2(Z) \\
 &= EF_0(Z) - EF_0^2(Z).
\end{aligned}
$$
Hence the result follows from the Slutsky's theorem.

</div>





<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).









