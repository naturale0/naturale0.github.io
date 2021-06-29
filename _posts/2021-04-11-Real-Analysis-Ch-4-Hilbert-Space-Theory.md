---
layout: post
title: "[Real Analysis] Ch 4. Hilbert Space Theory"
date:   2021-04-11 14:09:00 +0900
author: "Sihyung Park"
categories: [real analysis]

---

Objective of this chapter is to completely characterize $L^2(\mu),$ the famous Hilbert space. To achieve our goal, we will use the fact that a Hilbert space can be seen as an infinite-dimensional vector space where there exists a "orthogonal basis". i.e. any element in the space can be decomposed into an infinite linear combination of orthogonal components. In fact, the basis decomposition yields to the main result that $L^2$ is actually isomorphic to $\ell^2.$



- TOC
{:toc}
<br> 

## Counting measure

[TBD]

* countable $X$
* uncountable $X$



## Basic Hilbert space properties

### The element of the smallest norm

<div class="theorem" text="">
Let $E \sub H$ be a non-empty, closed, convex set. Then there uniquely exists $x \in E$ that satisfies
$$
\|x\| = \inf_{y \in E} \|y\|.
$$
</div>

<div class="proof"><br>
Let $M = \inf_{y \in E} \|y\|,$ then there exists $x_n \in E$ such that $\|x_n\| \to M.$ By the parallelogram law,
$$
\begin{aligned}
\|x_n - x_m\|^2 
 &= 2(\|x_n\|^2 + \|x_m\|^2) - \|x_n + x_m\|^2 \\
 &= 2(\|x_n\|^2 + \|x_m\|^2) - 4 \left\|\frac{x_n + x_m}{2}\right\|^2 \\
 &\le 2(\|x_n\|^2 + \|x_m\|^2) - 4M^2 \\
 &= 2(\|x_n\|^2 - m^2) + 2(\|x_m\|^2 - M^2)
\end{aligned}
$$
Third equality follows from convexity of $E.$ Note that $(x_n+x_m)/2 \in E.$ Since $\|\cdot\|$ is continuous, $\|x_n\|^2 \to M^2$ as $n$ goes to infinity. Thus $(x_n)$ is a Cauchy sequence in $H.$<br>

$H$ is a Hilbert space, which implies there exists $x \in H$ such that $x_n \to x.$ Again, by continuity of $\|\cdot\|,$ we get $\|x\|=M.$<br>

Now we need to show the uniqueness. Suppose there are $x,y\in H$ with $\|x\| = \|y\| = M.$ Then again by parallelogram law,
$$
\begin{aligned}
\|x-y\|^2 
 &= 2(\|x\|^2 + \|y\|^2) - \|x+y\|^2 \\
 &\le 2(M^2 + M^2) - 4M^2 = 0.
\end{aligned}
$$
Hence clearly $x=y.$

</div><br>

### Orthogonal decomposition

<div class="theorem" text="4.11. Orthogonal decomposition">

Let $M$ be a closed subspace of $H.$ For $x \in H,$ the followings hold.<br>

(i) There uniquely exists $P_x \in M$ and $Q_x \in M^\perp$ such that $x = P_x + Q_x.$<br>

(ii) $P_x, Q_x$ are the closeset point to $x$ from $M, M^\perp,$ respectively.<br>

(iii) $P_x, Q_x$ are linear.<br>

(iv) $\|x\|^2 = \|P_x\|^2 + \|Q_x\|^2.$

</div> 

<div class="proof"><br>
(i) Note that $M+x := \{y+x: y\in M\}$ is a non-empty, closed, convex set. Let $Q_x \in M+x$ be the element of the smallest norm in $M+x.$ Let $P_x = x - Q_x,$ then clearly $P_x \in M$ and $x = P_x + Q_x.$<br>

Now we only need to prove that $Q_x \in M^\perp.$ Observe that given $t \in \mathbb{R}$ and $z\in M,$ $Q_x + tz \in M+x.$ Thus
$$
\begin{aligned}
\|Qx\| &\le \|Q_x + tz\|, \\
\cancel{\|Q_x\|^2|} &\le \cancel{\|Q_x\|^2} + t^2\|z\|^2 + 2t(Q_x, z), \\
0 &\le t^2\|z\|^2 + 2t(Q_x, z).

\end{aligned}
$$
For the inequality to hold for all $t \in \mathbb{R},$ $(Q_x,z)$ should be zero for all $z\in M$, which implies $Q_x \in M^\perp.$

</div> <br>

### Characterization of continuous linear functional

<div class="theorem" text="4.12. characterization of continuous linear functional">

Let $L: H \to \mathbb{R}$ be a continuous linear functional. Then there uniquely exists $y\in H$ such that $Lx = (x, y).$

</div> 

<div class="proof"><br>
If $Lx = 0$ for all $x \in H,$ then trivially, let $y=0.$<br>

If $Lx \ne 0$ for some $x \in H,$ let $M = \{x: Lx = 0\},$ then since $L$ is continuous, $M$ is a closed subspace of $H$ and $M \ne H.$ We now claim that there exists $w \in M^\perp$ such that $w\ne 0.$<br>

For a given $x \in H \setminus M,$ there uniquely exists $P_x \in M$ and $Q_x \in M^\perp$ such that $x = P_x + Q_x.$ Let $u = Q_x \in M^\perp$ then $u \ne 0,$ otherwise contradiction.<br>

Let $w = (Lx)u - (Lu)x,$ then
$$
Lw = (Lx)(Lu) - (Lu)(Lx) = 0,
$$
thus $w \in M.$
$$
(w, u) = (Lx)\|u\|^2 - (Lu)(x, u) = 0, \\
Lx = \frac{Lu}{\|u\|^2}(x, u) = \left(x,  \frac{Lu}{\|u\|^2} u \right).
$$
Let $y = \frac{Lu}{\|u\|^2} u.$

</div> <br>



## Orthonormal basis of Hilbert space

### Existence of maximal orthonormal set

<div class="theorem" text="Hausdorff maximality theroem">

For any partially ordered set, there exists a maximal totally ordered subset.

</div><br>



<div class="theorem" text="existence of maximal orthonormal set">

Let $B \sub H$ be an orthonormal set in $H.$ Then there exists a maximal orthonormal set that contains $B.$

</div>  

<div class="proof"><br>
Let $\mathcal{P} = \{\text{orthonormal sets containing }B\}$ be a partially ordered set. By Hausdorff maximality theorem, there exists a maximal totally ordered subset $\mathcal{Q}.$ Define the candidate
$$
\mathcal{S} = \bigcup_{A \in \mathcal{Q}} A.
$$
Our claim is that $\mathcal{S}$ is the maximal orthonormal set. Clearly $B \sub \mathcal{S}.$ Now pick $u_1, u_2 \in \mathcal{S},$ then there exists $A_1, A_2 \in \mathcal{Q}$ so that $u_1 \in A_1$ and $u_2 \in A_2.$ Since $\mathcal{Q}$ is totally ordered, without loss of generality, we can say $A_1 \sub A_2.$ This implies $u_1, u_2 \in A_2$ and thus $(u_1, u_2) = 0.$<br>

Now, suppose $\mathcal{S}$ is not maximally orthonormal. Then there exists $u \in H$ such that 
$$
(u, u_\alpha) \text{ for all } u_\alpha \in \mathcal{S}.
$$
Then $\mathcal{Q} \cup \left\{\mathcal{S} \cup \{u_\alpha\}\right\}$ is also a totally ordered subset, which is a contradiction.

</div> <br>



### Orthonormal basis of Hilbert space

<div class="theorem" text="4.14. finite expansion">

$\{u_\alpha\}_{\alpha \in F}$ is an orthonormal set in $H,$ $F$ is finite. Define
$$
s_F(x) = \sum_{\alpha \in F} \hat x(\alpha) u_\alpha,\\
S=[\{u_\alpha\}_{\alpha \in F}].
$$
Then the followings hold.<br>

(i) $\|x - s_F(x)\| \le \|x - s\|$ for all $s \in S.$<br>

(ii) The equality in (i) holds only if $s = s_F(x).$<br>

(iii) $\sum_{\alpha \in F} \hat x(\alpha)^2 \le \|x\|^2.$

</div> 

<details>
  <summary>
    expand proof
  </summary>

<div class="proof"><br>
(i) and (ii). Note that $s_F(x) \in S$ and 
$$
(x-s_F(x), u_\alpha) = 0,~ \forall \alpha \in F.
$$
 This implies
$$
x - s_F(x) \in S^\perp.
$$
Hence, for given $s \in S,$
$$
\begin{aligned}
\|x - s\|^2
 &= \|x-s_F(x)\|^2 + \|s_F(x) - s\|^2.
\end{aligned}
$$
(iii) Put $s=0,$ then
$$
\begin{aligned}
\|x\|^2 
 &= \|x - s_F(x)\|^2 + \|s_F(x)\|^2 \\
 &\ge \|s_F(x)\|^2 = \sum_{\alpha \in F} |\hat x(\alpha)|^2.
\end{aligned}
$$
</div> 
</details><br>



<div class="theorem" text="4.17. general expansion">

Let $\{u_\alpha\}_{\alpha \in A}$ is an orthonormal set in $H,$ and define
$$
S=[\{u_\alpha\}_{\alpha \in A}].
$$
Then the followings hold.<br>

(i) $\sum_{\alpha \in A} |\hat x(\alpha)|^2 \le \|x\|^2.$<br>

(ii) $f:H \to \ell^2(A),$ $x \mapsto \hat x$ is linear and continuous.<br>

(iii) $\overline S \simeq \ell^2(A)$ with Hilbert space isomorphism $f.$

</div> 

<details>
  <summary>
    expand proof
  </summary>

<div class="proof"><br>

(i) 
$$
\sum_{\alpha \in F} \hat x(\alpha)^2 \le \|x\|^2,~ \forall \text{ finite } F.
$$
Thus 
$$
\sum_{\alpha \in A} \hat x(\alpha)^2 = \sup_{F \sub A:\text{ finite}} \sum_{\alpha \in F} \hat x(\alpha)^2 \le \|x\|^2.
$$
(ii) Linearity of $f$ is trivial. Now, observe that for given $x,y \in H,$
$$
\begin{aligned}
\|f(x) - f(y)\| 
 &= \|f(x-y)\| = \|\widehat{(x-y)}\| \\
 &\le \|x-y\|, 
\end{aligned}
$$
thus $f$ is Lipschitz continuous.<br>

(iii) For $f$ to be a Hilbert space isomophism, we need to prove that $f$ is isometric and surjective.<br>

(isometry) Given $x \in S,$ observe that $x$ is a (finite) linear combination, thus if we let $x = \sum_{\alpha \in F} c_\alpha u_\alpha$ for some finite $F,$
$$
\begin{aligned}
\|x\|^2
 &= \sum_{\alpha\in F} c_\alpha^2 \|u_\alpha\|^2 &&\text{($u_\alpha$'s are orthogonal)}\\
 &= \sum_{\alpha \in F} c_\alpha^2, &&\text{($\|u_\alpha\|$=1)}\\
\|\hat x\|^2
 &= \sum_{\alpha \in F} \hat x(\alpha) ^2 \\
 &= \sum_{\alpha \in F} c_\alpha^2. &&\text{($\hat x(\alpha) = c_\alpha$)}
\end{aligned}
$$
Hence the two values coincide.<br>

If $x \in \overline S,$ note that $\overline S$ is a closed subspace in $H,$ thus is a Hilbert space itself. There exists $x_n \in S$ such that $x_n \to x$ as $n \to \infty.$ Since $\|\cdot\|$ and $(\cdot)^2$ and $f$ are continuous,
$$
\|x_n\|^2 \to \|x\|^2, \\
\|x_n\|^2 = \|\widehat x_n\|^2, \\
\|\widehat x_n\|^2 \to \|\widehat x\|^2
$$
which implies $\|\widehat x\| = \|x\|.$<br>

(surjectivity) Theorem 3.13 implies that
$$
f(S) = \{s: \text{is simple},~ c(s\ne0) < \infty\}
$$
is dense in $\ell^2(A).$ Given $h \in \ell^2(A),$ there exists $h_n \in f(S)$ such that $h_n \to h.$ There also exists $x_n \in S$ such that $\widehat x_n = h_n.$ Note that since $\ell^2(A)$ is complete, this implies
$$
\begin{aligned}
&(h_n = \widehat x_n) \text{ is Cauchy}\\
\iff & (x_n) \text{ is Cauchy}  && \text{(isometry)} \\
\iff & x_n \to x \text{ for some } x \in \overline S &&\text{(Hilbert)}
\end{aligned}
$$
Thus $f$ is surjective.

</div>

 </details><br>



<div class="theorem" text="4.18. maximally orthonormal set yields a basis">
Let $\{u_\alpha\}_{\alpha \in A}$ is an orthonormal set in $H,$ and define
$$
S=[\{u_\alpha\}_{\alpha \in A}].
$$
Then the followings are equivalent.<br>

(i) $\{u_\alpha\}_{\alpha \in A}$ is a maximal orthonormal set.<br>

(ii) $\overline S = H.$<br>

(iii) $\|x\|^2 = \sum_{\alpha \in A}|\widehat x(\alpha)|^2$ for all $x \in H.$<br>

(iv) $(x,y) = \sum_{\alpha \in A} \widehat x(\alpha) \widehat y(\alpha)$ for all $x,y\in H.$

</div> 

<div class="proof"><br>
(i$\Rightarrow$ii) Suppose not. Then there exists $x \in H \setminus \overline S.$ Since $\overline S$ is a closed subspace, there is a unique decomposition $x = P_x + Q_x$ where $P_x \in \overline S$ and $Q_x \in \overline S ^\perp.$ Note that $Q_x \ne 0$ since otherwise $x \in \overline S$ which is a contradiction. Let $u = Q_x,$ then 
$$
\{u_\alpha\}_{\alpha \in A} \cup \{u\}
$$
is an orthonormal set, which is a contradiction.<br>

(ii$\Rightarrow$iii) By the previous theorem, it is trivial.<br>

(iii$\Rightarrow$iv) 
$$
\begin{aligned}
\|x+y\|^2
 &= \|x\|^2 + \|y\|^2 + 2(x,y), \\
\|\widehat x + \widehat y\| &= \|\widehat x\|^2 + \|\widehat y\|^2 + 2(\widehat x, \widehat y), \\
(x,y) &= (\hat x, \hat y) = \sum_{\alpha \in A} \widehat x(\alpha) \widehat y(\alpha).  && \text{($\|x\|=\|\hat x\|$)}
\end{aligned}
$$
(iv$\Rightarrow$i) Suppose not. Then there exists $u \in H$ that is orthogonal to $u_\alpha$ for all $\alpha \in A$ and $\|u\| = 1.$ i.e.
$$
\widehat u (\alpha) = (u, u_\alpha) = 0,~ \forall \alpha \in A.
$$
 Apply the result (iv), then
$$
\begin{aligned}
1 = (u,u) = \sum_{\alpha \in A} \widehat u(\alpha) \widehat u(\alpha) = 0.   &&(\Rightarrow\mspace{-4mu}\Leftarrow)
\end{aligned}
$$
</div>
</details><br>


### Fourier transform in $\ell^2(A)$

[TBD]



<br>

***References***

* Rudin. 1986. **Real and Complex Analysis**. 3rd edition. McGraw-Hill.
* **Real Analysis (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Insuk Seo).