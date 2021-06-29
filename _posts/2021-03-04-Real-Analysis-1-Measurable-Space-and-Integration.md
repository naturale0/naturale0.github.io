---
layout: post
title: "1. Measurable Space and Integration"
date:   2021-03-04 14:59:00 +0900
author: "Sihyung Park"
categories: [real analysis]
---



The `[Real Analysis]` series of posts is my memo on the lecture *Real Analysis (Spring, 2021)* by Prof. Insuk Seo. The lecture follows the table of contents of *Real and Complex Analysis (3rd ed.)* by Rudin, with minor changes in order.

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



<div class="prop" text="properties of $\sigma$-algebra">

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



<div class="remark"><br>

(i) If $f,g$ are measurable, then $\max\{f,g\}$ and $\min\{f,g\}$ are measurable.<br>

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



## Lebesgue integration

Now that we have a measure space, we define integration with respect to measures, or the **Lebesgue integration**. When it comes to defining the integration, since any measurable $f$ can be decomposed into positive functions $f^+$ and $f^-,$ it suffices to define integrals for positive functions.

<br>

<div class="definition" text="simple function"><br>
$s: X \to \mathbb{R},$ $s(x) = \sum_{i=1}^n \alpha_i \chi_{A_i}(x)$ is a simple function, if $A_1,\cdots,A_n \in \mathfrak{M}$ is a partition of $X$ and $\alpha_i \ne \alpha_j$ for all $i \ne j.$

</div> 

<br>

A simple function $s$ is measurable, since measurability of $A_i$'s implies measurability of $\chi_{A_i}$'s. We use a construction scheme called the **standard machine** to define Lebesgue integral. [Detailed flow and definition is described in the earlier blog post](/probability/PTE-1.4-Lebesgue-integral#lebesgue-integral), so I will not cover it again.

As I discussed at the end of the section of the linked post, (seamingly straightforward) additive property


$$
\int f + g ~d\mu = \int f d\mu + \int g d\mu
$$


requires a convergence theorem to be proved. We will prove it right at the next section. For now, additive property for integrals of simple functions can be easily shown.

<br>

<div class="lemma">

Let $s,t: X \to \overline{\mathbb{R}^+}$ be simple functions and $E \in \mathfrak{M}.$ Then
$$
\int_E s+t ~d\mu = \int_E s d\mu + \int_E t d\mu.
$$
</div> 

<br>

## Convergence theorems

### Monotone convergence theorem

Convergence theorems will be the most used utility throughout all chapters. Monotone convergence theorem (MCT) will be our starting point. Proof of MCT requires two lemmas.

<br>

<div class="lemma" text="1.25 (a)">
Let $s: X \to \overline{\mathbb{R}^+}$ be a simple function. Define $\varphi(E) = \int_E s~d\mu$ for all measurable $E.$ Then $\varphi$ is a measure on $(X, \mathfrak{M}).$

</div> 

<div class="lemma">
We write $E_n \uparrow E$ if $E = \cup_{n=1}^\infty E_n.$ If $E_n \uparrow E$ and $s$ is a simple function, then $\int_{E_n} s d\mu \uparrow \int_E s d\mu.$

</div> 

<br>



<div class="theorem" text="monotone convergence">

Let $(f_n)_{n=1}^\infty$ be a sequence of positive measurable funnctions such that $f_n \uparrow f$ to a positive function $f.$ Then<br>

(i) $f$ is measurable.<br>

(ii) $\int_X f_n d\mu \uparrow \int_X f d\mu.$

</div> 

<div class="proof"><br>
(i) Trivial since the pointwise limit of measurable functions is measurable.<br>

(ii) 
$$
\int_X f_n d\mu \le \int_X f d\mu,~ \forall n.
$$
Thus
$$
\lim_n \int_X f_n d\mu \le \int_X f d\mu \tag{1}.
$$
Now given a function $s$ such that $0 \le s \le f$ and $0<c<1,$ observe that $E_n := \\{ f_n \ge c\cdot s \\}$ is a measurable set. Since $f_n \uparrow f,$ $E_n \uparrow X$ as $n \to \infty.$
$$
\begin{aligned}
&\int_{E_n} c \cdot s ~d\mu \le \int_{E_n} f_nd\mu \le \int_X f_nd\mu \\
\overset{n\to\infty}\implies& \int_X c\cdot s ~d\mu \le \lim_n \int_X f_n d\mu \\
\overset{c\to1, \\ \sup_{0\le s\le f}}\implies& \int_X f d\mu \le \lim_n \int_X f_n d\mu.
\end{aligned} \tag{2}
$$
By (1) and (2), we get the desired result.

</div> 

<br>



### Results from MCT

Now the additive property of Lebesgue integral is direct from MCT.

<br>

<div class="lemma">
Let $f,g: X \to \overline{\mathbb{R}^+}$ be measurable functions. Then
$$
\int_X f+g ~d\mu = \int_X f d\mu + \int_X gd\mu.
$$
</div> 

<br>



Interchangeability between integral and infinite sum is also clear for positive measurable functions.

<br>

<div class="theorem" text="1.27">

Let $(f_n)_{n=1}^\infty$ be a sequence of positive measurable functions. Then
$$
\sum_{n=1}^\infty \int_X f_nd\mu = \int_X \sum_{n=1}^\infty f_n d\mu.
$$
</div> 

<br>



Similar to lemma 13, a measure can be constructed using any positive measurable function. (It will be covered in detail later as a *Radon-Nikodym derivative*.) 

<br>

<div class="theorem">

Let $f: X \to \overline{\mathbb{R}^+}$ be a measurable function and $E \in \mathfrak{M}.$ Define
$$
\varphi(E) := \int_E f~d\mu,
$$
then $\varphi$ is a measure and
$$
\int_X g ~d\varphi = \int_X g \cdot f~d\mu.
$$
</div>

<br> 

### Fatou's lemma

In order to use MCT, a sequence $f_n$ must converges to some function $f.$ Fatou's lemma relieves the condition and gives useful tool.

<br>

<div class="theorem" text="Fatou">

Let $(f_n)_{n=1}^\infty$ be a sequence of measurable functions. Then
$$
\int_X \liminf_n f_n d\mu \le \liminf_n \int_X f_n d\mu.
$$
</div> 

<div class="proof"><br>
$$
g_n := \inf_{k \ge n} f_k
$$

Use MCT with the fact $f_n \ge g_n.$

</div> 

<br>

### Dominated convergence theorem

Another useful convergence theorem is dominated convergence theorem (DCT).

<br>



<div class="theorem" text="1.32, 1.38">

Let $f,g \in L^1(\mu),$ then<br>

(i) $cf \in L^1(\mu)$ for $c\in\mathbb{R}$ and $\int cf~d\mu = c\int f ~d\mu.$<br>

(ii) $f+g \in L^1(\mu)$ and $\int f+g~d\mu = \int f ~d\mu + \int g ~d\mu.$<br>

(iii) $|\int f ~d\mu| \le \int |f|d\mu.$

</div> 

<br>



<div class="theorem" text="dominated convergence">

Let $(f_n)_{n=1}^\infty$ be a sequence of measurable functions such that $f_n \to f.$ Suppose there exists a measurable $g$ such that $|f_n| \le g$ for all $n.$ Then<br>

(i) $f \in L^1(\mu).$<br>

(ii) $\int_X |f_n-f| ~d\mu \to 0$ as $n \to \infty.$<br>

(iii) $\int_X f_nd\mu \to \int_X f~d\mu$ as $n\to\infty.$

</div> 

<div class="proof"><br>
(i) Clearly, $|f| \le g.$<br>

(ii)
$$
|f_n - f| \le |f_n| + |f| \le 2g, \\
2g - |f_n - f| \ge 0.
$$
 By Fatou's lemma,
$$
\begin{aligned}
\int_X \liminf_n \left( 2g - |f_n - f|\right) d\mu 
 &= \int_X 2g~d\mu \\
 &\le \liminf_n \int_X 2g-|f_n-f| ~d\mu \\
 &= \int_X 2g~d\mu - \limsup_n \int_X|f_n - f| ~d\mu

\end{aligned}
$$
hence
$$
\limsup_n \int_X |f_n - f| ~d\mu \le 0.
$$
(iii) Trivial by traingle inequality.

</div> 

<br>

## Complete measure space

<div class="definition" text="complete measure space"><br>
We say a measure space $(X, \mathfrak{M}, \mu)$ is complete, if 
$$
E \in \mathfrak{M},~ \mu(E)=0 \implies N \in \mathfrak{M} \text{ and } \mu(N) = 0,~ \forall N \subset E.
$$
</div>

<br>

One can build a complete measure space from a given measure space. We call such complete measure space a **completion** of it.

<br>

<div class="theorem" text="completion">

$$
\mathfrak{M}^* := \left\{E: A\subset E\subset B \text{ for some } A,B\in\mathfrak{M} \text{ s.t. } \mu(B\setminus A)=0\right\} \\
\mu^*(E) := \mu(A),~ \forall E \in \mathfrak{M}^*
$$

Then (i) $\mu^*$ is a well-defined measure and (ii) $(X, \mathfrak{M}^*, \mu^*)$ is a complete measure space.

</div> 

<div class="proof"><br>
(i) It is enough to show that for given sets $A, B, A', B'$ such that 
$$
A\subset E\subset B,~ \mu(B-A) = 0 \\
\text{ and } A'\subset E\subset B', \mu(B'-A')=0,
$$
we get $\mu(A) = \mu(A').$
$$
A-A' \subset E-A' \subset B'-A' \implies \mu(A-A') \le \mu(B'-A')=0, \\
A'-A \subset E-A \subset B-A \implies \mu(A-A') \le \mu(B-A)=0.
$$
Thus the result follows.<br>

(ii) First we show that $\mathfrak{M}^*$ is a $\sigma$-algebra. It is not difficult to show that $X \in \mathfrak{M}^*$ and $E^c \in \mathfrak{M}^*$ for $E \in \mathfrak{M}.$ Suppose $E_1,E_2,\cdots \in \mathfrak{M}^*.$ Then for given $i,$ there exist
$$
A_i \sub E_i \sub B_i,~ \mu(B_i-A_i) = 0.
$$
Then
$$
\cup_{i=1}^\infty A_i \sub \cup_{i=1}^\infty E_i \sub \cup_{i=1}^\infty B_i,~ \cup_{i=1}^\infty A_i, \cup_{i=1}^\infty B_i \in\mathfrak{M}^*
$$
and
$$
\begin{aligned}
\mu(\cup_{i=1}^\infty B_i - \cup_{i=1}^\infty A_i) 
 &\le \sum_{i=1}^\infty \mu(B_i-A_i) = 0.
\end{aligned}
$$
(iii)
$$
\begin{aligned}
\mu^*(\cup_{i=1}^\infty E_i) 
= \mu(\cup_{i=1}^\infty A_i)
= \sum_{i=1}^\infty \mu(A_i) 
= \sum_{i=1}^\infty \mu^*(E_i).
\end{aligned}
$$
</div> 

<br>

## Sets of Measure zero

### Almost everywhere

<div class="definition" text="almost everywhere"><br>
we call that the statement $S$ holds almost everywhere (a.e.), if there exists $E \in \mathfrak{M}$ such that $S$ hold on $E$ and $\mu(E^c) = 0.$

</div> 

<br>

<div class="definition" text="measurable function (extended)"><br>
Let $E \in \mathfrak{M}$ such that $\mu(E^c)=0.$ Then $f: E \to Y$ is a measurable function on $X,$ if 
$$
f^{-1}(V\cap E) \in \mathfrak{M},~ \forall \text{ open } V \sub Y.
$$
</div> 

If we define $\tilde f$ as an extension of $f$ such that $\tilde f(x) = 0$ for all $x \in E^c,$ then $\tilde f$ is measurable in terms of previous definition.

If the measure space is complete, any arbitrary extension of $f$ is measurable and 
$$
\int_X \tilde f ~d\mu = \int_E f ~d\mu.
$$
One can show that properties and theorems we discussed earlier in this chapter also holds for conditions relieved to be almost everywhere.

<br>

### Almost everywhere on $E$

<div class="definition" text="a.e. on a set"><br>
The statement $S$ holds a.e. on $E \in \mathfrak{M}$, if
$$
\mu \left( \{x \in E: S \text{ does not hold at } x\} \right).
$$
That is,
$$
\mu (S^c \cap E) = 0.
$$
</div> 

<br>

<div class="theorem" text="1.39 (a), (b)">

(i) $f \ge 0$ on $E \in \mathfrak{M},$ $\int_E f d\mu=0$ $\implies$ $f=0$ a.e. on $E.$<br>

(ii) $f \in L^1(\mu),$  $\int_E f d\mu = 0,$ $\forall E \in \mathfrak{M}$ $\implies$ $f=0$ a.e.

</div> 



<br>

***References***

* Rudin. 1986. **Real and Complex Analysis**. 3rd edition. McGraw-Hill.
* **Real Analysis (Spring, 2021)** @ Seoul National University, Republic of Korea (instructor: Prof. Insuk Seo).

