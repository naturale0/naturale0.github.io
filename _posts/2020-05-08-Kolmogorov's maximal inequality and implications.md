---
layout: post
title:  "Kolmogorov's maximal inequality and its implications"
date:   2020-05-09 01:12:00 +0900
categories: probability
---

Kolmogorov's maximal inequality provides result similar to that of Chebyshev's inequality to maximum of random series.

<div class="theorem" text="Kolmogorov's maximal inequality">
If $X_i$'s are independent, $EX_i=0$, $\mathrm{Var}(X_i) < \infty$, $S_n := \sum\limits_{k=1}^n X_k$, then the following inequality holds.

$$P(\max_{1 \leq k \leq n} |S_k| > x) \leq \frac{1}{x^2} \mathrm{Var}(S_n)$$

</div>


<div class="proof">
Let $A_k = \{ S_k > x,\: S_j \leq x,\: 1\leq j \leq n \}$. $A_k$'s are disjoint and $\bigcup\limits_{k=1}^n A_k = \{ \max_{1 \geq k \geq n} \|S_k\| > x \}$.

$$\begin{align} 
  \mathrm{Var}(S_n) &= \mathrm{E}(S_n^2) \geq \mathrm{E}(S_n^2; \cup_{k=1}^n A_k)\\
                                &= \sum\limits_{k=1}^n \int_{A_k} S_n^2 \: dP \\
                                &= \sum\limits_{k=1}^n \int_{A_k} (S_n - S_k + S_k)^2 \: dP \\
                                &= \sum\limits_{k=1}^n \int_{A_k} (S_n - S_k)^2 + S_k^2 + 2S_k (S_n - S_k) \: dP \\
                                &\geq \sum\limits_{k=1}^n \big\{ \int_{A_k} S_k^2 + 2\int_{\Omega}S_k\boldsymbol{1}_{A_k}\: dP \int_{\Omega}(S_n - S_k) \: dP \big\}\\
                                &= \sum\limits_{k=1}^n \int_{A_k} S_k^2 \: dP \\
                                &\geq \sum\limits_{k=1}^n \int_{A_k} x^2 \: dP \\
                                &= x^2P(\cup_{k=1}^n A_k) \\
                                &= x^2 P(\max_{1 \leq k \leq n} |S_k| > x)
\end{align}$$
</div>
<br>
Let $Y_n = X_{n+m}$ and $T_n= \sum\limits_{k=1}^n Y_k$, then $Y_i$'s are also independent with expectaion 0 and finite variance. Hence, the following also holds,

$$P(\max_{1 \leq k \leq n-m} |T_k| > x) \leq \frac{1}{x^2} \mathrm{Var}(T_{n-m})$$

which means

$$P(\max_{m \leq k \leq n} |S_k - S_m| > x) \leq \frac{1}{x^2} \mathrm{Var}(S_n - S_m)$$

Thus, even with different starting point of summation, and even if $X_i$'s are *not identically distributed*, the same form of inequality can be used. This result is useful when proving Kolmogorov's three-series theorem.
