---
layout: post
title:  "Application of Dynkin's π-λ theorem"
date:   2020-05-13 23:45:00 +0900
categories: [probability]
---

When dealing with collections of sets, Dynkin's systems provides simple but powerful tool for extension of properties in smaller collections to bigger ones.

First, we define $\pi$ and $\lambda$-systems.

<div class="definition" text="π-system">
A collection of sets $\mathcal{P}$ is a $\pi$-system if $A, B \in \mathcal{P}$, then $A \cap B \in \mathcal{P}$.

</div>

<div class="definition" text="λ-system">
A collection of sets $\mathcal{L}$ is a $\lambda$-system on $\Omega$ if the followings hold.
<br>
(1) $\Omega \in \mathcal{L}$
<br> 
(2) $A \in \mathcal{L} \Rightarrow A^c \in \mathcal{L}$
<br>
(3) $A_i \in \mathcal{L}, i=1,2,\cdots$, where $A_i$'s are disjoint. $\Rightarrow$ $\uplus_{i=1}^\infty A_i \in \mathcal{L}$
</div>

Note: Sometimes $\lambda$-system is referred to as **"Dynkin's system"**. There are more than two alternative definitions of $\lambda$-system. They are all equivalent and can be proved easily. Here, I introduce only one of them which I find myself the easiest to use when proving some collection of sets is a $\lambda$-system.

<br>

Then we state the main theorem. 

<div class="theorem" text="Dynkin's π-λ theorem">
$\mathcal{P}$ is a $\pi$-system and $\mathcal{L}$ is a $\lambda$-system. If $\: \mathcal{P} \subset \mathcal{L}$, then $\sigma(\mathcal{P}) \subset \mathcal{L}$.
</div>

<br>

Here, $\sigma(\mathcal{P})$ is the smallest $\sigma$-field containing $\mathcal{P}$.

With the theorem, if some property holds for a $\pi$-system $\mathcal{P}$, we can extend the same property to be hold for $\sigma(\mathcal{P})$. I will review three examples.

<br>


<div class="theorem" text="equivalent probability measures">
$\mu_1$, $\mu_2$ are probability measures on $(\Omega, \mathcal{F})$. $\mathcal{A} \subset \mathcal{F}$ is a $\pi$-system such that $\sigma(\mathcal{A}) = \mathcal{F}$. If $\mu_1(A) = \mu_2(A)$, $\forall A \in \mathcal{A}$, then $\mu_1 \overset{A \in \mathcal{F}}{\equiv} \mu_2$.
</div>

<div class="proof">
Let $\mathcal{L} = \{ B \in \mathcal{F} : \mu_1(B) = \mu_2(B) \}$, then by construction $\mathcal{A} \subset \mathcal{L}$ and it is clear that $\mathcal{L}$ is a $\lambda$-system. By $\pi-\lambda$ theorem, $\sigma(\mathcal{A}) = \mathcal{F} \subset \mathcal{L}$ leads to the desired results.
</div>

<br>

<div class="theorem" text="extension of independence">
$\mathcal{A}, \mathcal{B}$ are $\pi$-systems and are subsets of $\mathcal{F}$. If $\mathcal{A}, \mathcal{B}$ are independent, then $\sigma(\mathcal{A}), \sigma(\mathcal{B})$ are independent.
</div>

<div class="proof">
Let $\mu$ be a probability measure on $(\Omega, \mathcal{F})$. For a given $A \in \mathcal{A}$, let $\mathcal{L}_A = \{ B \in \mathcal{F}:  \mu(A \cap B) = \mu(A)\mu(B) \}$. Then $\mathcal{L}_A$ is a $\lambda$-system that contains $\mathcal{B}$ and $\sigma(\mathcal{B}) \subset \mathcal{L}_A$. Since $A \in \mathcal{A}$ was arbitrarily chosen, it is independent to $\mathcal{A}$.
<br>
&ensp; Now for given $B \in \sigma(\mathcal{B})$ let $\mathcal{L}_B = \{ A \in \mathcal{F}: \mu(A \cap B) = \mu(A)\mu(B) \}$. Then similar to the above, $\mathcal{L}_B$ is a $\lambda$-system that contains $\mathcal{A}$ and $\sigma(\mathcal{A}) \subset \mathcal{L}_B$, which leads to the desired result.
</div>


<br>

The last example does not actually utilize $\pi-\lambda$ theorem, but is uses similar idea on its proof.

<div class="theorem" text="extension to random variable">
$\mathcal{A} \subset \mathcal{F}$ satisfies $\sigma(\mathcal{A}) = \mathcal{B}(\mathbb{R})$. $X: (\Omega, \mathcal{F}) \to (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ is a function defined on a probability space. If $X^{-1}(A) \in \mathcal{F}$, $\forall A \in \mathcal{A}$, then $X$ is a random variable.
</div>
