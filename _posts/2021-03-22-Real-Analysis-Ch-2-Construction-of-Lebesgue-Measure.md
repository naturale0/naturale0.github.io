---
layout: post
title: "[Real Analysis] Ch 2. Construction of Lebesgue Measure"
date:   2021-03-22 10:50:00 +0900
author: "Sihyung Park"
categories: [real analysis]
---



In this chapter, we construct the Lebesgue measure on $\mathbb{R}^d.$ For this, we prove Riesz representation theorem and use the result to construct a complete measure space $(\mathbb{R}, \mathfrak{M}, m)$ such that integration with respect to $m$ is equal to Riemann integration for all Riemann-integrable functions. We then use $\sigma$-compactness of $\mathbb{R}$ to show that such $m$ is the Lebesgure measure.



- TOC
{:toc}
<br> 

<u>Throughout chapter 2, without any further description, I will denote compact sets by $K$ or $H,$ open sets by $U$ or $V$ and closed sets by $F.$</u>

<br>



## Topological preliminaries



### Hausdorff space

<div class="definition" text="Hausdorff"><br>
A space $X$ is Hausdorff, if for all $x,y \in X,$ there exist $U,V \sub X$ such that $x \in U,$ $y \in V$ and $U \cap V = \phi.$

</div> 

<br>

<div class="theorem" text="2.6. finite intersection property">

For a Hausdorff $X$ and $\{K_i\}_{i \in I}$ such that $\cap_{i\in I} K_i = \phi,$
$$
\exists \text{ a finite }J \text{ s.t. } \cap_{i\in J} K_i = \phi.
$$
</div> 

<br>

### Locally compactness

<div class="definition" text="locally compactness"><br>
$X$ is locally compact, if
$$
\forall x \in X, \exists U \text{ such that } x\in U \text{ and } \overline U \text{ is compact.}
$$
</div> 

<br>

### Locally compact & Hausdorff

<div class="definition"><br>
(i) 
$$
C_c(X) := \{f:X\to\mathbb{R},~ f \text{ is continuous and } \text{supp.}f \text{ is compact}\}
$$
where $\text{supp.}f:= \overline{\{ f > 0\}}.$<br>

(ii) We write $K \prec f,$ if $f \in C_c(X),$ $0 \le f \le 1$ and $f=1$ on $K.$<br>

(iii) We write $f \prec V,$ if $f \in C_c(X),$ $0 \le f \le 1$ and $\text{supp.}f \sub V.$

</div> 

<br>

The following three theorems are being used frequently.

<br>

<div class="theorem" text="2.7">

For a locally compact Hausdorff space $X$ and $K \sub U \sub X,$
$$
\exists V \text{ such that } K \sub V \sub \overline V \sub U.
$$
</div>

<br>

<div class="theorem" text="2.12 Urysohn">

For a locally compact Hausdorff space $X$ and $K \sub V \sub X,$
$$
\exists f \in C_c(X) \text{ such that } K \prec f \prec V.
$$
</div> 

<br>

<div class="theorem" text="2.13. partition of unity">

For a locally compact Hausdorff space $X,$ $K \sub X$ and open cover $\{V_1,\cdots,V_n\}$ of $K,$
$$
\exists h_1,\cdots,h_n \in C_c(X) \text{ such that } 
h_i \prec V_i, ~\forall i \text{ and } K \prec \sum_{i=1}^n h_i.
$$
</div> 

<br>

## Riesz representation theorem

Riesz representation theorem (RRT) states that positive linear functional defined on $C_c$ of locally compact Hausdorff space can be represented as Lebesgue integral with respec to some complete measure space.

<br>

<div class="theorem" text="Riesz">

Let $X$ be a locally compact Hausdorff space, and $\Lambda: C_c(X) \to \mathbb{R}$ be a positive linear functional. Then there exists a $\sigma$-algebra $\mathfrak{M}$ that contains all Borel sets and uniquely exists a measure $\mu$ that satisfies the followings.<br>

(i) $\Lambda f = \int_X f d\mu,$ for all $f \in C_c(X).$<br>

(ii) $\mu(K) < \infty,$ for all compact $K.$<br>

(iii) $\mu(E) = \inf\{\mu(V): E \sub V,~ V \text{ is open}\},$ for all $E \in \mathfrak{M}.$<br>

(iv) $\mu(E) = \sup\{\mu(K): K\sub E,~ K \text{ is compact }\},$ for all $E \in \mathfrak{M}$ such that $\mu(E) < \infty$ for $E$ is open.<br>

(v) $(X, \mathfrak{M}, \mu)$ is complete.

</div> 

<div class="remark">
(i) The representation is well-defined since $f$ is Borel measurable beause it is continuous.<br>
(ii) Note that the codomain of $\Lambda$ is $\mathbb{R},$ which implies $\Lambda f < \infty$ for all $f \in C_c(X).$<br>

(iii) This is called <b>outer regularity</b>, which means measure of some sets can be approximated by larger open sets.<br>

(iv) This is called <b>inner regularity</b>, which means measure of some sets can be approximated by smaller compact sets.<br>

(+) We say $(X, \mathfrak{M}, \mu)$ is <b>regular</b>, if all Borel sets are inner <u>and</u> other regular. We will later show that if $X$ is in addition a $\sigma$-compact space, then $(X, \mathfrak{M}, \mu)$ is regular.

</div>

<br>

## Proof of RRT

Proof of the theorem is quite long and exhaustive. I would like to divide it into 11 steps.

The first step is to prove uniqueness of such $\mu.$ The last step is to prove that such measure space satisfies $\Lambda f = \int_X f d\mu.$ These two steps are not as intercorrelated as the steps inbetween, so I will only number the 9 steps inbetween these two.

We define


$$
\mu(V) := \sup\{\Lambda f: f \prec V\}, \\
\mu(E) := \inf\{\mu(V): E \sub V\}, \\
\mathfrak{M}_F := \left\{E \sub X: \mu(E) > \infty,~ \mu(E) = \sup\{\mu(K): \text{compact }K \sub E\}\right\} \\
\mathfrak{M} := \{E \sub X: E \cap K \in \mathfrak{M}_F,~ \forall \text{ compact } K\}.
$$


Then show the followings one at a time.

1. $\mu\left( \cup_{i=1}^\infty E_i \right) \le \sum_{i=1}^\infty \mu(E_i)$ for all $E_i \sub X.$
2. $\mu(K) = \inf \\{\Lambda f: K \prec f\\}.$  
    Hence $\mu(K) < \infty$ and $K \in \mathfrak{M}_F.$ 
3. Any open $V$ is inner regular.  
    Hence if $\mu(V) < \infty,$ then $V \in \mathfrak{M}_F.$
4. $\mu\left( \cup_{i=1}^\infty E_i \right) = \sum_{i=1}^\infty \mu(E_i)$ for disjoint $E_i \in \mathfrak{M}_F.$ And if $\mu(E) < \infty,$ then $E \in \mathfrak{M}_F.$
5. For a given $E \in \mathfrak{M}_F$ and $\epsilon > 0,$ there exists $K, V$ such that $K \sub E \sub V$ and $\mu(V \setminus K) < \epsilon.$
6. If $A, B \in \mathfrak{M}_F,$ then $A\setminus B,$ $A \cap B,$ $A\cup B \in \mathfrak{M}_F.$
7. $\mathfrak{M}$ is a $\sigma$-algebra containing all Borel sets.
8. $\mathfrak{M}_F = \\{E\in\mathfrak{M}: \mu(E)< \infty\\}.$
9. $\mu\left( \cup_{i=1}^\infty E_i \right) = \sum_{i=1}^\infty \mu(E_i)$ for disjoint $E_i \in \mathfrak{M}.$

<br>

### Uniqueness of $\mu$

Suppose $\mu_1, \mu_2$ are measures that satisfies the conditions.<br>

**Claim 1:** If $\mu_1(K)=\mu_2(K)$ for all compact $K,$ then $\mu_1(E) = \mu_2(E)$ for all $E \in \mathfrak{M}.$

<div class="proof" text="claim 1"><br>

Given an open $V,$
$$
\begin{aligned}
\mu_1(V)
 &= \sup \left\{ \mu_1(K): \text{compact } K \sub V \right\} \\
 &= \sup \left\{ \mu_2(K): \text{compact } K \sub V \right\} \\
 &= \mu_2(V).
\end{aligned}
$$
Now, given an $E \in \mathfrak{M},$
$$
\begin{aligned}
\mu_1(E)
 &= \sup \left\{ \mu_1(V): \text{open } V \supset E \right\} \\
 &= \sup \left\{ \mu_2(V): \text{open } V \supset E \right\} \\
 &= \mu_2(E).
\end{aligned}
$$
</div> 

<br>

**Claim 2:** $\mu_1(K) = \mu_2(K),~ \forall \text{ compact }K.$

<div class="proof" text="claim 2"><br>

For a given $\epsilon > 0,$ by outer regularity there exists $V$ such that $K \sub V$ and $\mu_2(V) \le \mu_2(K) + \epsilon.$ By Urysohn's lemma, there exists $f$ such that $K \prec f \prec V.$
$$
\begin{aligned}
\mu_1(K) 
 &= \int_X \chi_K d\mu_1  \\
 &\le \int_X f d\mu_1 = \Lambda f \\
 &= \int_X f d\mu_2 \\
 &\le \int_X \chi_V d\mu_2  \\
 &= \mu_2(V) \le \mu_2(K) + \epsilon.
\end{aligned}
$$
Similarly, one can show that $\mu_2(K) \le \mu_1(K) + \epsilon.$ By letting $\epsilon \downarrow 0,$ we get the result.

</div> 

<br>

### 1. $\mu\left( \cup_{i=1}^\infty E_i \right) \le \sum_{i=1}^\infty \mu(E_i)$ for all $E_i \sub X$

<u>Partition of unity</u> plays an important part of the proof. 



**(1) $\mu(V_1 \cup V_2) \le \mu(V_1) + \mu(V_2).$**

<div class="proof"><br>
Given $g \prec V_1 \cup V_2,$ and let $K=\text{supp.}g$ be a compact set. Then by partition of unity, there exists $h_1,h_2 \in C_c(X)$ such that $h_i \prec V_i,$ $i=1,2$ and $K \prec h_1 + h_2.$ Thus
$$
g(x) = g(x)\left(h_1(x) + h_2(x)\right), \\
\Lambda g = \Lambda(g\cdot h_1) + \Lambda(g \cdot h_2)
$$
Take supremum to $g$ on both sides, and we get
$$
\mu(V_1 \cup V_2) \le \mu(V_1) + \mu(V_2).
$$
</div> 

**(2) By induction, $\mu(\cup_{i=1}^n V_i) \le \sum_{i=1}^n \mu(V_i).$**

**(3) $\mu\left( \cup_{i=1}^\infty E_i \right) \le \sum_{i=1}^\infty \mu(E_i).$**

<div class="proof"><br>
For given $\epsilon >0,$ there exists $V_i \supset E_i$ such that $\mu(V_i) \le \mu(E_i) + \frac{\epsilon}{2^i}.$ Take $f$ such that $f \prec \cup_{i=1}^\infty V_i.$ Since $\text{supp.}f$ is compact, there exists $n$ such that $f \prec \cup_{i=1}^n V_i.$
$$
\begin{aligned}
\Lambda f 
 &= \mu\left( \cup_{i=1}^n V_i \right) \\
 &\le \sum_{i=1}^n \mu(V_i) \\
 &\le \sum_{i=1}^\infty \mu(V_i) \\
 &\le \sum_{i=1}^\infty \mu(E_i) + \epsilon.
\end{aligned}
$$
Taking supremum to $f$ to both sides gives
$$
\mu\left(\cup_{i=1}^\infty E_i\right) \le \mu\left(\cup_{i=1}^\infty V_i\right) \le \sum_{i=1}^\infty \mu(E_i) + \epsilon.
$$
Letting $\epsilon \downarrow 0$ gives the desired result.

</div> 

<br>

### 2. $\mu(K) = \inf \\{\Lambda f: K \prec f\\}$

It is equivalent to show that (1) $\mu(K) \le \Lambda f$ for all $f: K \prec f$ and (2) for given $\epsilon > 0,$ there exists $f \prec K$ such that $\mu(K) \ge \Lambda f - \epsilon.$

**(1) $\mu(K)$ is a lower bound of $\Lambda f,$ $K \prec f.$** 

<div class="proof"><br>
Given $f \succ K,$ let $V_\alpha = \{f > \alpha\}$ for $\alpha < 1.$ Then since $f$ is continuous, $V_\alpha$ is open. Since $f > \alpha$ on $V_\alpha,$ $\alpha g \le f$ hence $\alpha \Lambda f \le \Lambda f$ for $g \prec V_\alpha.$
$$
\mu(K) \le \mu(V_\alpha) = \sup \{\Lambda g: g \prec V_\alpha\} \le \frac{1}\alpha \Lambda f.
$$
Letting $\alpha \to 1,$ we get the result.

</div> 

**(2) $\mu(K)$ is the greatest lower bound of $\Lambda f$, $K \prec f.$**

<div class="proof"><br>
Given $\epsilon > 0$. By outer regularity, there exists $V$ such that $K \sub V$ and $\mu(V) \le \mu(K) + \epsilon.$ By Urysohn's lemma, there exists $f$ such that $K \prec f \prec V.$ By definition of $\mu,$ 
$$
\begin{aligned}
\Lambda f &\le \mu(V) \\
 &\le \mu(K) + \epsilon.
\end{aligned}
$$
</div> 



Hence $\mu(K) \le \Lambda f \in \mathbb{R}$ thus is finite and $K \in \mathfrak{M}_F.$

<br>

### 3. $V$ is inner regular

<div class="proof"><br>
Given $\epsilon > 0.$ It suffices to show that there exists $K \sub V$ such that $\mu(V) - \epsilon \le \mu(K).$ Let $\alpha = \mu(V) - \epsilon,$ then by definition of $\mu,$ there exists $f$ such that $f \prec V$ and $\Lambda f > \alpha.$ Let $K = \text{supp.} f$ be a compact set. To show that $\mu(K) \ge \Lambda f,$ we will use the fact
$$
\mu(K) = \inf\{\mu(U): K \sub U\} \text{ and} \\
\mu(U) = \sup\{\Lambda g: g \prec U\}.
$$
 Take $U \supset K,$ then by definition $f \prec U$ and
$$
\Lambda f \le \mu(U) := \sup\{\Lambda g: g \prec U\}.
$$
 Thus by taking infimum to $\mu(U),$ $U \supset K$ to both sides, we get
$$
\Lambda f \le \inf \{\mu(U): U \supset K\} = \mu(K).
$$
</div> 



Hence if $\mu(V) < \infty,$ then $V \in \mathfrak{M}_F.$



<br>

### 4. $\mu$ is $\sigma$-additive on $\mathfrak{M}_F~$ & $~\mu(E) < \infty \Rightarrow E \in \mathfrak{M}_F$

Since we already proved 1., it suffices to show the other side of inequality. For this, we will divide the proof into substeps similar to that in 1.

**(1) $\mu(K_1 \cup K_2) \ge \mu(K_1) + \mu(K_2),$ $K_1,K_2$ are disjoint.** 

<div class="proof"><br>
Observe that $K_1 \sub K_2^c$ and $K_2^c$ is open. By Urysohn's lemma, there exists $f$ such that $K_1 \prec f \prec K_2^c.$ Using the result from 2., for given $\epsilon >0$ there exists $g$ such that $K_1 \cup K_2 \prec g$ and $\Lambda g \le \mu(K_1 \cup K_2) + \epsilon.$ Thus
$$
K_1 \prec f\cdot g \text{ and } K_2 \prec (1-f)\cdot g
$$
and
$$
\begin{aligned}
\mu(K_1) + \mu(K_2) 
 &\le \Lambda(f\cdot  g) + \Lambda((1-f)\cdot g) \\
 &= \Lambda g \le \mu(K_1 \cup K_2) + \epsilon.
\end{aligned}
$$
By letting $\epsilon \to 0,$ the result follows.

</div> 

**(2) By induction, $\mu\left(\cup_{i=1}^n K_i\right) \ge \sum_{i=1}^n \mu(K_i)$ for disjoint $K_i$'s**

**(3) $\mu\left( \cup_{i=1}^\infty E_i \right) \ge \sum_{i=1}^\infty \mu(E_i),$ $E_i \in \mathfrak{M}_F$ are disjoint.**

<div class="proof"><br>
For $E_i$, by inner regularity there exists $K_i \sub E_i$ such that $\mu(K_i) \ge \mu(E_i) - \frac{\epsilon}{2^i}.$
$$
\begin{aligned}
\mu\left( \cup_{i=1}^\infty E_i \right)
 &\ge \mu\left( \cup_{i=1}^n E_i \right) \\
 &\ge \mu\left( \cup_{i=1}^n K_i \right) \\
 &\ge \sum_{i=1}^n \mu(K_i) \\
 &\ge \sum_{i=1}^n \mu(E_i) - \epsilon.
\end{aligned}
$$
By letting $\epsilon \to 0,$ we get the result.

</div> 

If $\mu(E) < \infty,$ then for all $\epsilon>0,$ there exists $N\in\mathbb{N}$ such that 


$$
\begin{aligned}
\mu(E) 
 &\le \sum_{i=1}^N \mu(E_i) + \epsilon \\
 &\le \sum_{i=1}^N \mu(K_i) +2\epsilon \\
 &= \mu\left(\cup_{i=1}^N K_i\right) + 2\epsilon.
\end{aligned}
$$


This implies $E$ is inner regular, hence $E \in \mathfrak{M}_F.$

<br>

### 5. $\forall E \in \mathfrak{M}_F,$ $\forall \epsilon > 0,$ $\exists K, V$ such that $K \sub E \sub V$ and $\mu(V \setminus K) < \epsilon$

<div class="proof"><br>
By outer regularity,
$$
\exists V \supset E \text{ such that } \mu(V) \le \mu(E) + \epsilon/2.
$$
By inner regularity,
$$
\exists K \sub E \text{ such that } \mu(E) \le \mu(K) + \epsilon/2.
$$
Since $K \sub V,$ note that $V = K \cup (V\setminus K).$
$$
\begin{aligned}
 K \text{ is compact} &\implies K \in \mathfrak{M}_F,\\
 V\setminus K \text{ is open and }&\\
 \mu(V\setminus K) \le \mu(V) < \mu(K) + \epsilon < \infty 
 &\implies V \setminus K \in \mathfrak{M}_F.
\end{aligned}
$$
By 4., it suffices to show that $\mu(V) - \mu(K) < \epsilon.$
$$
\mu(V) = \mu(K) + \mu(V \setminus K), \\
\mu(V \setminus K) = \mu(V) - \mu(K) \le \epsilon.
$$
</div> 

<br>

### 6. If $A, B \in \mathfrak{M}_F,$ then $A\setminus B,$ $A \cap B,$ $A\cup B \in \mathfrak{M}_F$

**(1) $A \setminus B \in \mathfrak{M}_F.$**

<div class="proof"><br>
Given $\epsilon > 0,$ by 5. there exist $K_1 \sub A \sub V_1$ and $K_2 \sub B \sub V_1$ such that $\mu(V_1\setminus K_1) < \epsilon $ and $\mu(V_2 \setminus K_2) < \epsilon.$ Then
$$
A \setminus B \sub (V_1 \setminus K_1) \cup (V_2 \setminus K_2) \cup (K_1 \setminus V_2).
$$
By 1.,
$$
\begin{aligned}
\mu(A \setminus B)
 &\le \mu(V_1 \setminus K_1) + \mu(V_2 \setminus K_2) + \mu(K_1 \setminus V_2) \\
 &\le \mu(K_1 \setminus V_2) + 2\epsilon < \infty
\end{aligned}
$$
since $K := K_1 \setminus V_2$ is compact. This implies $A\setminus B$ is inner regular and its measure is finite, thus $A \setminus B \in \mathfrak{M}_F.$

</div> 

**(2) $A\cap B, A\cup B \in \mathfrak{M}_F$**

<div class="proof"><br>
$$
A \cap B = A \setminus(A\setminus B) \in \mathfrak{M}_F, \\
A \cup B = A \cup (B\setminus A) \in \mathfrak{M}_F.
$$

</div> 

<br>

### 7. $\mathfrak{M}$ is a $\sigma$-algebra containing all Borel sets

<div class="proof"><br>
It is not difficult to show that $\mathfrak{M}$ is a $\sigma$-algebra. Now it is enough to show that all closed sets are contained in $\mathfrak{ M}.$ Given a closed $F,$
$$
\begin{aligned}
F \cap K \subset K 
&\implies F \cap K \text{ is compact}, \forall K \\
&\implies F \cap K \in \mathfrak{M}_F, \forall K
\end{aligned}
$$
</div> 

<br>

### 8. $\mathfrak{M}_F = \\{E\in\mathfrak{M}: \mu(E)< \infty\\}$

It is clear that $E \in \mathfrak{M}_F$ implies $E \in \mathfrak{M}.$

**ETS:** $E \in \mathfrak{M},$ $\mu(E) < \infty.$ $\implies$ $E$ is inner regular.

<div class="proof"><br>
Given $\epsilon > 0,$ there exists $V \supset E$ such that $\mu(V) \le \mu(E) + \epsilon < \infty.$ Thus such $V \in \mathfrak{M}_F.$ By 5., there exists $K \subset V$ such that $\mu(V \setminus K) \le \epsilon.$<br>

For such $K,$ by definition of $\mathfrak{M},$ $E \cap K \in \mathfrak{M}_F.$ Then by inner regularity, there exists a compact $H \sub (E\cap K)$ such that 
$$
\mu(E\cap K) \le \mu(H) + \epsilon.
$$
 Note that $E \sub (E \cap K) \cup (V \setminus K),$ thus 
$$
\mu(E) \le \mu(E\cap K) + \mu(V\setminus K) \le \mu(K) + 2\epsilon
$$
which makes $E \in \mathfrak{M}_F.$

</div> 

<br>

### 9. $\mu$ is a measure on $(X, \mathfrak{M})$

**ETS:** $\mu\left( \cup_{i=1}^\infty E_i \right) = \sum_{i=1}^\infty \mu(E_i)$ for disjoint $E_i \in \mathfrak{M}.$

<div class="proof"><br>
If $\mu(E_i) = \infty$ for some $E_i,$ then it is trivial.<br>

Otherwise, it implies $E_i \in \mathfrak{M}_F$ for all $i=1,2,\cdots.$ Thus by 4., it is clear.

</div> 

<br>

### $\Lambda f = \int_X f d\mu$ for all $f \in C_c(X)$

<div class="proof"><br>
<p>Observe that if $\Lambda f \le \int_X fd\mu,$ then by applying this to $-f$ we get $\Lambda f \ge \int_X f d\mu.$ Thus it suffices to show that $\Lambda f \le \int_X f d\mu.$</p>

<p>Given $f \in C_c(X),$ let $K=\text{supp.}f$ be a compact set. Since $f$ is continuous, by min-max theorem $f(X) = f(K)$ is compact in $\mathbb{R}$. Thus there exists $a, b \in \mathbb{R}$ such that $f(K) \sub (a, b].$</p>

<p>For a small enough $\epsilon > 0,$ Let

$$
a=y_0<y_1<\cdots<y_n = b,\\
y_i-y_{i-1} < \epsilon,~ \forall 1\le i\le n.
$$

</p>

<p>Let $E_i = f^{-1}(y_{i-1}, y_i] \cap K \in \mathfrak{M}$ so that $\{E_1,\cdots,E_n\}$ be a partition of $K.$ Then by Outer regularity, there exist open $W_i$'s such that 

$$
E_i \sub W_i,~ \mu(W_i) \le \mu(E_i) + \epsilon/n.
$$

In addition, let
$$
U_i = f^{-1}(y_{i-1}, y_i+\epsilon),~ 1\le i\le n
$$
be open sets. Finally, let
$$
V_i = W_i \cap U_i.
$$
Then clearly the followings hold.
$$
\begin{aligned}
&\text{(1) } E_i \sub V_i,~ \forall i \\
&\text{(2) } f \in (y_{i-1}, y_i) \text{ on } V_i,~ \forall i \\
&\text{(3) } \mu(V_i) \le \mu(E_i) + \epsilon / n
\end{aligned}
$$
</p>

(1) implies that $(V_1,\cdots, V_n)$ is an open cover of $K.$ By partition of unity, there exist $h_1,\cdots,h_n \in C_c(X)$ such that $h_i \prec V_i$ for all $i$ and $K \prec \sum_{i=1}^n h_i.$ With the result from 2., this implies
$$
\mu(K) \le \Lambda \left( \sum_{i=1}^n h_i \right)
$$
Note that since $K$ is the support of $f,$
$$
f = f\cdot \sum_{i=1}^n h_i = \sum_{i=1}^n f\cdot h_i
$$
and since $h_i \prec V_i,$
$$
f \cdot h_i \le (y_i + \epsilon)\cdot h_i.
$$
Thus
$$
\begin{aligned}
\Lambda f
 =& \sum_{i=1}^n \Lambda \left( f \cdot h_i \right) \\
 \le& \sum_{i=1}^n (y_i + \epsilon)\Lambda (h_i) \\
 =& \sum_{i=1}^n (y_i + \epsilon + |a|) \Lambda (h_i) - |a|\sum_{i=1}^n \Lambda(h_i) \\
 \le& \sum_{i=1}^n (y_i + \epsilon + |a|) \mu (V_i) - |a| \Lambda\left(\sum_{i=1}^n h_i\right) \\
 \le& \sum_{i=1}^n (y_i + \epsilon + |a|)\left(\mu(E_i) + \frac{\epsilon}{n}\right) - |a|\mu(K) \\
 =& \sum_{i=1}^n (y_i-\epsilon)\cdot\mu(E_i) + 2\epsilon\mu(K) + \cancel{|a|\mu(K)} \\
 &+ \frac{\epsilon}{n}\sum_{i=1}^n (y_i + \epsilon + |a|) \\
 &- \cancel{|a|\mu(K)} \\
 \le& \int_X f d\mu + \epsilon\left( 2\mu(K) + |b| + |a| + \epsilon \right).
\end{aligned}
$$
Letting $\epsilon\to0$ yields the desired result.

</div> 











<br>

***References***

* Rudin. 1986. **Real and Complex Analysis**. 3rd edition. McGraw-Hill.
* **Real Analysis (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Insuk Seo).