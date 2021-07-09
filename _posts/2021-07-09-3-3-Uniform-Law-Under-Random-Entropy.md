---
layout: post
title: "3.3. Uniform Law Under Random Entropy"
date:   2021-07-09 11:33:00 +0900
author: "Sihyung Park"
categories: [empirical process, asymptotics, Empirical Processes in M-estimation]
---



Using all the lemmas from 3.2 to 3.5, we prove another sufficiency of the uniform law: the vanishing random entropy condition. This condition is fairly weaker than the finite bracketing entropy condition in two senses. First, instead of the (sup-normed) envelope condition, it only requires the envelope to be integrable. In $L^p(Q)$ where $Q$ is a finite measure, this is clearly implied by the envelop condition. In addition, [as we already saw before](/2021/07/06/2-2-Entropy#entropy-with-bracketing-for-the-lp-norm), the vanishing random entropy is implied by the finite bracketing entropy condition. 

In fact, van de Geer (2000) named this condition simply "the random entropy condition", but I did a small modification to the naming. The author did not clearly mention why the condition is called "random". I think this is because the entropy is computed with respect to the empirical measure $P_n,$ which is constructed by a *random* sample, hence becomes *random* itself.

<br>

- TOC
{:toc}
<br> 

## Lemma 3.6 ($L^2$ condition)

First let's prove the result in the stronger condition ($L^2$ case).

<div class="lemma" text="3.6">
<p>
    (a) $\sup_{g\in\mathcal G} \|g\|_\infty < R$ for some $0\le R<\infty.$
</p>



<p>
    (b) $\frac1n H_{2,P_n}(\delta,\mathcal G) \overset P \to 0$ for all $\delta>0.$
</p>

If (a) and (b) holds, then $\mathcal G$ satisfies the ULLN.

</div> 

<div class="proof"><br>
First, note that $\left|\int g~d(P_n-P)\right|$ is a non-negative martingale. Suppose that
$$
\sup_{g\in\mathcal G}\left|\int g~d(P_n-P)\right| \overset P \to 0,
$$
then by <a href="/2020/12/27/PTE-4.2-martingales#martingale-convergence-theorems-1">the martingale convergence theorem</a>, it follows that
$$
\sup_{g\in\mathcal G}\left|\int g~d(P_n-P)\right| \to 0 \text{ a.s.} \tag{ULLN}
$$
Therefore it is enough to show convergence to zero in probability. Note in addition that for given $\delta>0,$ for $n \ge 8R^2/\delta^2,$
$$
\mathbb P\left( \sup_{g\in\mathcal G} \bigg| \int g~d(P_n-P) \bigg| > \delta \right) \le 4 \mathbb P\left( \sup_{g\in\mathcal G} \bigg| \frac1n\sum_{i=1}^nW_ig(X_i) \bigg| > \frac\delta4 \right).
$$
Thus it suffices to show that
$$
\mathbb P\left( \sup_{g\in\mathcal G} \bigg| \frac1n\sum_{i=1}^nW_ig(X_i) \bigg| > \delta \right) \overset P\to 0,~ \forall \delta>0.
$$
Although we cannot apply the maximal inequality directly to the left-hand side, we can apply it to the conditional probability
$$
\mathbb P\left( \sup_{g\in\mathcal G} \bigg| \frac1n\sum_{i=1}^nW_ig(X_i) \bigg| > \frac\delta4 ~\Bigg\vert~ A_n \right)
$$
where
$$
A_n:=\left\{ \mathbf X:~ R\vee R\cdot H^{1/2}_{2,P_n}(\delta/32,\mathcal G) \le \frac{\sqrt n \delta}{8C} \right\}
$$
for some constant $C$. This is because each condition from (a) to (c) is satisfied as follows:
$$
\begin{aligned}
\text{(a)}~
 & W_i\gamma_i \in \{-|\gamma_i|, |\gamma_i|\},~ \forall i.\\
 & \text{Hoeffding's inequality implies that}\\ 
 &~~~~\mathbb P\left(| W^\intercal \gamma | \ge a\right) \le 2\exp\left( -\frac{a^2}{2\|\gamma\|^2} \right),~ \forall a>0. \\
 &\text{Hence, let } C_1=2, C_2=\sqrt2. \\
\text{(b)}~
 & \sup_{g\in\mathcal G} \|g\|_{2,P} \le \sup_{g\in\mathcal G} \|g\|_{\infty} < R. \\
\text{(c)}~
 & \text{Let } \varepsilon=\frac\delta8. \text{ Then on } A_n, \\
 &~~~~ C\left(\int_{\delta/32}^R H^{1/2}_{2,P_n}(u,\mathcal G)du \vee R\right) \\
 &~~~~\le C\left( R\cdot H^{1/2}_{2,P_n}(\delta/32,\mathcal G) \vee R \right) \le \frac{\sqrt n\delta}8.
\end{aligned}
$$
By the maximal inequality,
$$
\begin{aligned}
&\mathbb P\left( \sup_{g\in\mathcal G} \bigg| \frac1n \sum_{i=1}^n W_ig(X_i) \bigg| > \frac\delta4 \right) \\
&\le \mathbb P\left( \sup_{g\in\mathcal G} \bigg| \frac1n \sum_{i=1}^n W_ig(X_i) \bigg| > \frac\delta4,~ A_n \right) + \mathbb P(A_n^c) \\
&= \mathbb E_\mathbf{X} \mathbb P\left( \sup_{g\in\mathcal G} \bigg| \frac1n \sum_{i=1}^n W_ig(X_i) \bigg| > \frac\delta4, ~A_n ~\Bigg|~\mathbf X \right) + \mathbb P(A_n^c) \\
&\le C\exp\left( -\frac{n\delta^2}{8^2C^2R^2} \right) + \mathbb P\left( \frac1nH_{2,P_n}(\delta/32,\mathcal G) > \frac\delta{8CR} \right) \\
&\to 0.
\end{aligned}
$$
</div> 

<br>

## Theorem 3.7 (main theorem; $L^1$ condition)

Now we prove the main theorem using this result.

<div class="theorem" text="3.7. ULLN under vanishing random entropy">

<p>
    (a) $\sup_{g\in\mathcal G} \|g\|_1 < \infty.$
</p>



<p>
    (b) $\frac1n H_{1,P_n}(\delta,\mathcal G) \overset P \to 0$ for all $\delta>0.$
</p>

If (a) and (b) holds, then $\mathcal G$ satisfies the ULLN.

</div> 

<div class="proof"><br>
To utilize the lemma 3.6, we define a truncated version of $\mathcal G.$ For given $R>0,$ let
$$
\mathcal G_R = \left\{ g\mathbf 1_{(G \le R)}:~ g\in\mathcal G \right\}.
$$
Then the $L^2$ norm is bounded from above by the $L^1$ norm
$$
\int_{G\le R} (g_1-g_2)^2 dP_n \le 2R\int |g_1-g_2|dP_n
$$
so we have the vanishing $L^2$ entropy.
$$
\frac1n H_{2,P_n}(\delta,\mathcal G_R) \overset P\to 0,~ \forall \delta>0.
$$
By the lemma 3.6, $\mathcal G_R$ satisfies the ULLN for all $R>0.$ <br><br>

Now what is left is proving that the ULLN still holds even if $R\to\infty.$
$$
\begin{aligned}
&\sup_{g\in\mathcal G} \bigg| \int g~d(P_n-P) \bigg| \\
 &\le \color{darkblue}{ \sup_{g\in\mathcal G} \bigg| \int_{G\le R} g~d(P_n-P) \bigg| }
  + \color{darkgreen}{ \int_{G>R} G~dP_n }
  + \color{darkred}{ \int_{G>R} G~dP }. \\
\end{aligned}
$$
For given $\delta>0,$ take $R>0$ large enough so that
$$
\color{darkred}{ \int_{G>R} G~dP } \le \delta.
$$
Then take $n\in\mathbb N$ large enough so that
$$
\color{darkgreen}{ \int_{G>R} G~dP_n } \le \delta \text{ a.s.} ~\text{ and } \color{darkblue}{ \sup_{g\in\mathcal G} \bigg| \int_{G\le R} g~d(P_n-P) \bigg| } \le \delta \text{ a.s.}
$$
Then the desired result follows.

</div> 









<br>

***References***

* van de Geer. 2000. **Empirical Processes in M-estimation**. Cambridge University Press.
* **Theory of Statistics II (Fall, 2020)** @ Seoul National University, Republic of Korea (instructor: Prof. Jaeyong Lee).