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

***Throughout chapter 2, without any further description, I will denote compact sets by $K,$ open sets by $U,V$ and closed sets by $F.$***



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

The following three theorems are used frequently.

<br>

<div class="theorem" text="2.7">

For a locally compact Hausdorff space $X$ and $K \sub U \sub X,$
$$
\exists V \text{ such that } K \sub V \sub \overline V \sub U.
$$
</div>

<br>

<div class="theorem" text="2.12 Uryshon">

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

[TBD]















<br>

***References***

* Rudin. 1986. **Real and Complex Analysis**. 3rd edition. McGraw-Hill.
* **Real Analysis (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Insuk Seo).