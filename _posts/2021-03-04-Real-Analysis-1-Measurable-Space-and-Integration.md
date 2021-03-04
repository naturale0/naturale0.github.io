---
layout: post
title: "[Real Analysis] Ch 1. Measurable Space and Integration"
date:   2021-03-04 14:59:00 +0900
author: "Sihyung Park"
categories: [real analysis]

---

This is a lecture note of *Real Analysis (Spring, 2021)* by Prof. Insuk Seo. The lecture follows the table of contents of *Real and Complex Analysis (3rd ed.)* by Rudin, with minor changes in order.

In the first chapter, we define measurablility, measure, Borel space and integration with respect to a measure. The first part will be a mere list of definitions and properties and I will skip proofs that are easy to be shown.



- TOC
{:toc}
<br> 



## Measurable space

We want to define a "measure" that measures the "volumes" of subsets of $\mathbb{R}.$ By volumes, i meant a function $\mu$ with the following properties.


$$
\begin{aligned}
&\text{(i) }   \mu([0,1]) = 1.\\
&\text{(ii) }  A,B \text{ are disjoint } \implies \mu(A\cup B) = \mu(A) + \mu(B). \\
&\text{(iii) } A \equiv B \implies \mu(A) = \mu(B).
\end{aligned}

\tag{1}
$$




We start by defining measurable spaces: candidates for a domain of "measure" functions.

<div class="definition" text="measurable space"><br>

For a set $X$, a collection of subsets of $X$ $\mathfrak{M}$ is a $\sigma$-algebra of $X$ if <br>
(i) $X \in \mathfrak{M}.$<br>
(ii) $A \in \mathfrak{M} \implies A^c \in \mathfrak{M}.$<br>
(iii) $A_1,A_2,\cdots \in \mathfrak{M} \implies \cup_{i=1}^\infty A_i \in \mathfrak{M}.$

</div>

We say a set $A$ is measurable if $A \in \mathfrak{M}.$ For any set $X$, we can easily derive two $\sigma$-algebras.

1. $\mathfrak{M}_1 := \\{\phi, X\\}.$
2. $\mathfrak{M}_2 := 2^X.$

The first one is called the *trivial $\sigma$-algebra*, and the second is called the *discrete $\sigma$-algebra*. Measures in trivial $\sigma$-algebra of $\mathbb{R}$ is unimportant since their properties are not so complicated. Measure with property (1) in discrete $\sigma$-algebra of $\mathbb{R}$ cannot be defined and it is proved as [the Banach-Tarski paradox](https://en.wikipedia.org/wiki/Banach%E2%80%93Tarski_paradox). Our focus of interest will be non-trivial $\sigma$-algebras that are inbetween these two. As an example of such, we can easily prove that $\mathfrak{M}_3 := \\{A \subset X: A \text{ or } A^c \text{ is countable}\\}$ is a $\sigma$-algebra. ($\mathfrak{M}_3$ is sometimes called a *countable-cocountable $\sigma$-algebra*.)

The following properties are direct from the definition and basic properties of set operations.



<div class="prop" text="properties of $\sigma$-algebra"><br>

(i) $\phi \in \mathfrak{M}.$<br>
(ii) $A_1,A_2,\cdots \in \mathfrak{M} \implies \cap_{i=1}^\infty A_i \in \mathfrak{M}.$<br>
(iii) $A, B \in \mathfrak{M} \implies A\setminus B \in \mathfrak{M}.$

</div>  

<br>



## Measurable functions

<div class="definition" text="topology"><br>
For a set $X$, a collection of subsets $\tau$ is a topology on $X$ if<br>

(i) $\phi, X \in \tau.$ <br>
(ii) $A_i \in \tau,~ i \in I \implies \cup_{i \in I} A_i \in \tau.$<br>
(iii) $A_1,\cdots,A_n \in \tau \implies \cap_{i=1}^n A_i \in \tau.$

</div> 

We call $(X, \tau)$ a topological space and say a subset $V$ is *open in $X$* if $V \in \tau.$ Similar to that from the above, we can define trivial and discrete topology for all sets. In addition, we can always define topology from a metric space $(X, d)$ by defining open sets as sets that are countable unions of open balls.

Properties of functions usually follows, and named after, that of image/preimage of them. Measurable functions are functions that have inverse images of open sets as measurable sets.

<div class="definition" text="measurable function"><br>

$(X, \mathfrak{M})$ is a measurable space, $(Y, \tau)$ is a topological space. $f: X \to Y$ is a measurable function if $f^{-1}(V) \in \mathfrak{M}$ for all $V \in \tau.$
</div>



Our first theorem states that composition with continuous function preserves measurability of functions.



<div class="theorem" text="1.7">

$X$ is a measurable space and $Y$ is a topological space. $g: Y \to Z$ is continuous. Then<br>

(i) $f: X \to Y$ is continous $\implies$ $(g\circ f)$ is continuous.<br>
(ii) $f: X \to Y$ is measurable $\implies$ $(g \circ f)$ is measurable.

</div> 



Another useful theorem is about composition with multivariate function.



<div class="theorem" text="1.8">

$f, g : X \to \mathbb{R}$ are measurable functions. $\Phi: \mathbb{R}^2 \to Y$ is a continuous mapping to topological space $Y.$ Then $h(x) := \Phi\left(f(x), g(x)\right)$ is measurable.

</div> 

The proof uses the general fact that any open set in $\mathbb{R}^2$ can be represented as a countable union of rectangles. Theorem (1.8) is important since it results in common operations such as addition to retain measurability of functions. In addition, since any complex function $f$ can be represented with two real functions $u, v$ as $f = u + iv$, it is (mostly) enough to study real functions.



<div class="theorem" text="1.9">

If $f: X \to \mathbb{C}$ is measurable, there exists a complex measurable function $\alpha: X \to \mathbb{C}$ such that<br>

(i) $|\alpha|=1.$<br>

(ii) $f = \alpha |f|.$

</div> 

<div class="proof"><br>
Let $\alpha = \varphi(f + \chi_E)$, where $E = \{f=0\}$ and $\varphi(z) = z/|z|.$ Then $\alpha$ is measurable and satisfies the conditions.

</div> 



Limits of measurable functions are also measurable, if exists. For the discussion, we think of functions in extended real number system $\overline{\mathbb{R}}$. To prove so, we need this lemma.



<div class="lemma" text="1.12(c)">

For $f: X \to \overline{\mathbb{R}},$ $f$ is measurable if and only if $f^{-1}(a, \infty] \in \mathfrak{M}$ for all $a \in \mathbb{R}.$

</div>



With the help of the lemma, we get

<div class="theorem" text="1.14">

Let $(f_n: X \to \overline{\mathbb{R}})_{n=1}^\infty$ be a sequence of measurable functions. Then the followings are also measurable.<br>

(i) $\sup_n f_n.$<br>

(ii) $\inf_n f_n.$<br>

(iii) $\limsup_n f_n.$<br>

(iv) $\liminf_n f_n.$<br>

</div> 

<div class="proof"><br>
Since $\inf_n f_n = - \sup_n (-f_n)$ and $\liminf,$ $\limsup$ are defined as $\sup$ and $\inf,$ it is enough to prove that $\sup_n f_n$ is measurable. It comes directly from


$$
\{\sup_n f_n > a \} = \{ f_n > a \text{ for some } n\in\mathbb{N}\}.
$$


</div> 



And finally,

<div class="corollary">

If $f_n$'s are measurable and $\lim_n f_n = f,$ then $f$ is measurable.

</div> 



Using the facts, we can generalize positive functions to functions. Details are on the remark.



<div class="remark">
    
</div>

(i) If $f,g$ are measurable, then $\max\\{f,g\\}$ and $\min\\{f,g\\}$ are measurable.<br>

(ii) $f$ is measurable if and only if $f^+, f^-$ are measurable, where 
$$
f^+ := \max\{f, 0\},~ f^- := -\min\{f, 0\}.
$$
</div>



Rationale behind decomposition of $f$ into $f^+$ and $f^-$ not by other positive functions are by the following proposition.



<div class="prop">
Let $g, h$ be positive functions so that $f = g - h.$ Then $g \ge f^+$ and $h \ge f^-.$
</div> 



Thus $f^+$ and $f^-$ is a positive functions that decomposes $f$ without superflous information.

<br>



## Borel $\sigma$-algebra

In real number system, in many cases we want open sets to be measurable sets. Borel $\sigma$-algebra is the minimal $\sigma$-algebra that contains all open sets. The existence of it is trivial by the theorem.



<div class="theorem" text="1.10">

For a set $X$ and a collection of subsets $\mathcal{F},$ there exists the smallest $\sigma$-algebra $\mathfrak{M}^*$ that contains $\mathcal{F}.$
</div> 

<div class="proof"><br>
$$
\mathfrak{M}^* := \bigcap_{\mathcal{F} \subset \mathfrak{M},\\\mathfrak{M} \text{ is a } \sigma\text{-alg}} \mathfrak{M}.
$$

</div> 



<div class="definition" text="Borel set"><br>
For a topological space $(X, \tau),$ $\mathcal{B}:= \cap_{\tau \subset \mathfrak{M}} \mathfrak{M}$ is the Borel $\sigma$-algebra. $B \in \mathcal{B}$ is a borel set. For a topological space $Y,$ $f:X\to Y$ is a borel function if $f^{-1}(V) \in \mathcal{B}$ for all open $V \subset Y.$

</div> 



Borel $\sigma$-algebras are important non-trivial $\sigma$-algebras that are inbetween $\mathfrak{M}_1$ and $\mathfrak{M}_2.$ Notable examples of Borel sets include, but not limited to [$F_\sigma$](https://en.wikipedia.org/wiki/F%CF%83_set) and [$G_\delta$](https://en.wikipedia.org/wiki/G%CE%B4_set) sets. By definition, all continuous functions are Borel functions. On $\mathbb{R},$ Borel sets include sets of the form $(a, b],$ [a, b) and $\\{\frac{1}{n}: n\in\mathbb{N}\\}.$ In fact, almost all sets that we can imagine are Borel sets.



The next theorem generalizes the results until now.



<div class="theorem" text="1.12">

$(X, \mathfrak{M})$ is a measurable space, $Y, Z$ are topological spaces, and $Y$ is equipped with Borel $\sigma$-algebra $\mathcal{B}.$ Then<br>

(i) For $f: X \to Y,$ $\Omega:=\{E \subset Y: f^{-1}(E) \in \mathfrak{M}\}$ is a $\sigma$-algebra.<br>

(ii) For a measurable $f: X \to Y,$ $f^{-1}(E) \in \mathfrak{M}$ for $E \in \mathcal{B}.$ <br>

(iii) For a measurable $f: X \to Y$ and a Borel $g: Y \to Z,$ $h:=(g \circ f)$ is measurable.

</div> 



<br>

## Measures

For simplicity, denote $\overline{\mathbb{R}^+}=[0, \infty].$

<div class="definition" text="positive measure">

 For a measurable space $(X, \mathfrak{M}),$ a function $\mu: \mathfrak{M} \to \overline{\mathbb{R}^+}$ is a measure, if<br>

(i) <b>($\sigma$-additivity)</b> $A_1,A_2,\cdots \in \mathfrak{M}$ are disjoint $\implies \mu(\cup_{i=1}^\infty A_i) = \sum_{i=1}^\infty \mu(A_i).$<br>

(ii) $\mu(E) < \infty$ for some $E \in \mathfrak{M}.$

</div>

We say a measurable space equipped with a measure $(X, \mathfrak{M}, \mu)$ a *measure space*. The second condition is for non-trivial result (to avoid $\mu(E)=\infty$ for all measurable $E$). Throughout this lecture, we merely denote "measures" for positive measures unless otherwise noted. If codomain of such function is $\mathbb{R},$ we call it a real measure. Similarly, for such function of codomain $\mathbb{C},$ we call it a complex measure.



<div class="prop" text="properties of measures">
(i) $\mu(\phi) = 0.$<br>

(ii) $A_1,\cdots,A_n$ are disjoint $\implies$ $\mu(\cup_{i=1}^n A_i) = \sum_{i=1}^n \mu(A_i).$<br>

(iii) $A \subset B$ $\implies$ $\mu(A) \le \mu(B).$ <br>

(iv) <b>(continuity from below)</b> $A_n \uparrow A$ $\implies$ $\mu(A_n) \uparrow \mu(A).$<br>

(v) <b>(continuity from above)</b> $A_n \downarrow A,$ $\mu(A_1) < \infty$ $\implies$ $\mu(A_n) \downarrow \mu(A).$

</div> 

<div class="proof"><br>
(i) through (iii) are trivial. For (iv), consider $B_i := A_i \setminus A_{i-1}$ for $i \ge 2.$ For (v), consider $C_i := A_1 \setminus A_i.$

</div> 



Examples of measures include counting measure and Lebesgue measure. Counting measure $c$ counts the number of elements of sets. To be specific, For a measurable space $(X, \mathfrak{M})$ where $\mathfrak{M}=2^X,$


$$
c(E) = \begin{cases}
  |A|,~ A \text{ is finite.} \\
  \infty,~ A \text{ is infinite.}
\end{cases}
$$


Lebesgue measure $m$ (on $\mathbb{R}$) is the one that satisfy (1) and will be our focus in the later chapter.


$$
m\left((a,b)\right) = b-a,~~ a<b\in\mathbb{R}.
$$


<br>



## (To be appended)



<br>

***References***

* Rudin. 1986. **Real and Complex Analysis**. 3rd edition. McGraw-Hill.
* **Real Analysis (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Insuk Seo).

