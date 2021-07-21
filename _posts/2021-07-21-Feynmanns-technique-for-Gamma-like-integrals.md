---
layout: post
title: "Feynmann's technique for Gamma-like integrals"
date:   2021-07-21 17:06:00 +0900
author: "Sihyung Park"
categories: [mathematical analysis]
---



In mathematical statistics and probability theory, integration of the form that resembles gamma function arises time to time if not frequently:


$$
\Gamma(k;\theta):=\int_0^\infty x^{k-1}e^{-\theta x}dx,~ k\in\mathbb N.
$$
 

If $\theta=1,$ then it is the gamma function. The notation $\Gamma(k;\theta)$ is *not* a standard one. I wanted to make relationship with gamma function clear.

I recently encountered this form (with $k=3$) when trying to compute variance of standard logistic distribution. Without second thoughts, I applied integration by parts to solve such integrals. Although integration by parts solved the problem, unfolding the integral revealed its recurring form, which means it can be computed in much easier way. However, trying to derive the general form for any values of $k$ using integration by parts was a lot of labor.

In turns out, the famous [Feynmann's integral trick](https://www.cantorsparadise.com/richard-feynmans-integral-trick-e7afae85e25c) can be applied (and proved) to this form without a hassle.

**First**, let the integral of exponential part as a function in $\theta.$ That is, denote integral by


$$
I(\theta) = \int_0^\infty e^{-\theta x}dx = \left[-\frac1\theta e^{-\theta x}\right]_0^\infty = \frac1\theta. \label{1}\tag{1}
$$


**Second**, observe that differentiating $I(\theta)$ multiple times with respect to $\theta$ yields the integral we wants to solve. This is because the integrand and its derivative is continuous in both $\theta$ and $x$ so that by the Leibniz rule we can interchange integration and differentiation.


$$
\begin{aligned}
\frac{\partial^{k-1}}{\partial\theta^{k-1}}I(\theta)
 &= \int_0^\infty \frac{\partial^{k-1}}{\partial^{k-1} \theta} e^{-\theta x} dx \\
 &= \int_0^\infty (-1)^{k-1} x^{k-1} e^{-\theta x}dx \\
 &=\begin{cases}
 \Gamma(k;\theta),& \text{$k$ is even} \\
 -\Gamma(k;\theta),& \text{$k$ is odd}
 \end{cases}
\end{aligned}
$$


**Finally**, link this with the fact $\eqref{1}.$ We can easilly achieve the following.


$$
\Gamma(k;\theta) = (k-1)!\frac{1}{\theta^k}.
$$


