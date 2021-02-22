---
layout: post
title:  "Limitation of $R^2$"
date:   2020-04-28 18:37:10 +0900
author: "Sihyung Park"
category: linear model
---

<div class="fact" text='limitation of coefficient of determination'>
For a linear regression $y_i = \beta_0 + \sum\limits_{j=1}^{p} \beta_j x_{ij}$, $1 \leq i \leq n$, suppose $x_{ij}$'s does not have any relationship with $y_i$'s. i.e. true model is $y_i = \beta_0 = \bar{y}$. Under this assumption,

$$\begin{align*}
    \frac{\mathrm{SSE}}{\sigma^2} &\sim \chi^2(n-p-1) \overset{D}{=} \Gamma(\frac{n-p-1}{2}, 2)\\
    \frac{\mathrm{SSR}}{\sigma^2} &\sim \chi^2(p) \overset{D}{=} \Gamma(\frac{p}{2}, 2)\\   
    \mathrm{SSE} &\perp \mathrm{SSR}
\end{align*}$$

Thus, $R^2 = \frac{\mathrm{SSR}}{\mathrm{SSR} + \mathrm{SSE}} \sim \mathcal{B}(\frac{p}{2}, \frac{n-p-1}{2})$, and $E(R^2) = \frac{p}{n-1}$.
</div>



Hence expectation of $R^2$ increases as the dimension of predictors increases, regardless of fit of the model.



<div id="related" class="clearfix">
  <br><br>
<hr>
   <h3>Related Posts</h3>
  <ul>
    <li><a href="/probability/PTE-2.4-strong-law-of-large-numbers">(PTE) 2.4. Strong law of large numbers</a></li>
    <li><a href="/probability/PTE-3.4-central-limit-theorem">(PTE) 3.4. Central limit theorem</a></li>
    <li><a href="/probability/PTE-2.3-B-C-lemmas">(PTE) 2.3. Borel-Cantelli lemmas</a></li>
    <li><a href="/probability/Kolmogorov_s-maximal-inequality-with-shifted-starting-point">"Kolmogorov's maximal inequality with shifted starting point"</a></li>
    <li><a href="/probability/PTE-3.3-characteristic-functions">(PTE) 3.3. Characteristic functions</a></li>
  </ul>
</div>