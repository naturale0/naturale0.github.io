---
layout: post
title:  "High-dimensional box"
date:   2020-04-24 18:37:10 +0900
author: "Sihyung Park"
categories: probability
---

<div class="example" text='High-dimensional box'>
Consider an $n$-dimensional box $[-1, 1]^n$. Suppose we randomly pick an element from this box. i.e. $\mathbf{X_n}=(X_1, \cdots, X_n)$, where $X_1, \cdots, X_n \stackrel{iid}{\sim} \mathcal{U}(-1,1)$. Then as $n \to \infty$, $P(\sqrt{\frac{n}{3}(1-\epsilon)}< \|\mathbf{X_n}\|_2 < \sqrt{\frac{n}{3}(1+\epsilon)}) \to 1$, $\forall{0<\epsilon<1}$.
</div>



This implies that the probability of observing the element at the surface of the box becomes 1 as the dimension increases. This is one of the properties of high-dimensional problems which makes them challenging.


<div id="related" class="clearfix">
  <br><br>
<hr>
   <h3>Related Posts</h3>
  <ul>
    <li><a href="/bayesian/machine%20learning/natural%20language%20processing/LDA-4-Gibbs-Sampling">Understanding Latent Dirichlet Allocation (4) Gibbs Sampling</a></li>
    <li><a href="/probability/PTE-2.4-strong-law-of-large-numbers">(PTE) 2.4. Strong law of large numbers</a></li>
    <li><a href="/machine%20learning/natural%20language%20processing/Understanding-Neural-Probabilistic-Language-Model">Understanding Neural Probabilistic Language Model</a></li>
    <li><a href="/bayesian/machine%20learning/natural%20language%20processing/LDA-3-Variational-EM">Understanding Latent Dirichlet Allocation (3) Variational EM</a></li>
    <li><a href="/machine%20learning/setting-up-m1-mac-for-both-tensorflow-and-pytorch">Setting up M1 Mac for both TensorFlow and PyTorch</a></li>
  </ul>
</div>