---
layout: post
title: "Understanding Restricted Boltzmann Machine"
date:   2021-07-13 17:53:00 +0900
author: "Sihyung Park"
categories: [machine learning, information theory, generative]
---



A Boltzmann machine is an unsuperviced generative model that learns the probability distribution of a random variable using the Boltzmann distribution. Although it has been proposed in 1985, practical utilization was nearly impossible for samples of nontrivial sizes. Only later in 2002 when the restricted version of it overcame the implausibility did it became a widely used algorithm.



- TOC
{:toc}
<br> 

## Boltzmann machine

We will consider the simplest version here: The one without any hidden units.

Let $\mathbf x=(x_1,\cdots,x_m)^\intercal \in \mathbb \{0, 1\}^m$ be a realization of a <u>binary</u> $m$-dimensional random vector following the distribution $P.$ Each entry $x_i$ will become a unit (node) of the network (Boltzmann machine) that is visible (observable). One can interpret that the unit $x_i$ is "on" if $x_i=1$ and is "off" otherwise. Suppose that we have a training data $\\{\mathbf x_\ell:~ 1\le \ell\le L\\}$ of size $L.$ Our goal is to learn $p$ using the data at hand. A (unrestricted) Boltzmann machine (BM) models the distribution with the Boltzmann distribution with product of Boltzmann constant $k$ and temperature $T$ set to $kT=1$ and the energy $E(\mathbf x)$ of the visible (observed) sample $\mathbf x$ follows the formula below.


$$
\hat p(\mathbf x) = \frac {e^{-E(\mathbf x)}} Z,~~ Z=\sum_{\mathbf x} e^{-E(\mathbf x)},
$$

$$
E(\mathbf x) = \color{blue}{ -\sum_{1\le i<j\le m} w_{ij}x_ix_j } \color{green}{ -\sum_{i=1}^m a_ix_i } 
\tag{1}\label{1}
$$


where $w_{ij}$ is the strength of connection between the $i$th element and the $j$th element and $a_i$ is a threshold. I would like to comment on the three main concepts regarding the model. 

<br>

### 1. Strength of connection

In Boltzmann machine setting, we assume that $w_{ij}=w_{ji}$ which makes it a **symmetric Hopfield network**. This can be represented as a graph.



<div style="text-align:center">
<img src="/assets/fig/210713_BM.png" alt="boltzmann.png" width="350"/>
<br>
<em>Figure 1. A Boltzmann machine with visible units only</em>
</div><br>
<br>

### 2. Energy

The energy $E(\mathbf x)$ is assigned to each global state of the network. I will directly quote Wikipedia for the rationale behind the naming "energy". If you are interested in the original explanation, see Hopfield (1982).



> This quantity is called "energy" because it either decreases or stays the same upon network units being updated. Furthermore, under repeated updating the network will eventually converge to a state which is a [local minimum](https://en.wikipedia.org/wiki/Local_minimum) in the energy function. (...) Thus, if a state is a local minimum in the energy function it is a stable state for the network.       ([Hopfield network, Wikipedia](https://en.wikipedia.org/wiki/Hopfield_network#Energy))



Hopfield (1982) derived a local minimizer as follows.


$$
\begin{cases}
w_{ij} = \frac1L \sum_{\ell=1}^L x_{\ell i} x_{\ell j} \\
a_i = \frac1L \sum_{\ell=1}^L x_{\ell i}
\end{cases}
$$


For the Hopfield solution, the suggestion of such energy formula follows from the **Hebb's rule**, which is a neuroscientific theory that accounts for neuronal plasticity. The punchline of the rule is that "neurons wire together if they fire together". This is because $w_{ij}$ is a sample correlation and $a_i$ is a sample mean of $\mathbf x_\ell$: 


$$
\begin{aligned}
\color{blue}{ \sum_{1\le i<j\le m} w_{ij}x_ix_j } 
 ~&\text{increases as the sample correlation $w_{ij}$} \\
 &\text{and the correlation of an unseen sample $x_ix_j$ coincides}\\

\color{green}{ \sum_{i=1}^m a_ix_i } 
 ~&\text{increases as the sample mean $a_i$} \\
 &\text{and the value of an unseen sample $x_j$ coincides}
\end{aligned}
$$

<br>

### 3. Threshold

Define the **local energy** $E(x_k) := -\sum_{i}w_{ki}x_kx_i - a_kx_k$ **at the $k$-th unit**. Then in the symmetric connection setting, the **energy gap at the $k$-th unit** is computed as


$$
\Delta E(x_k) = E(x_k=1)-E(x_k=0) = \sum_i w_{ki}x_i - a_k.
$$


Notice that during the learning process, the model tends to turn the $k$-th unit *on* if the surrounding signal $\sum_i w_{ki}x_i$ of the unit $x_k$ is stronger than the value $a_k.$ This is why we call the term "threshold" (Ackley et al., 1985).

<br>

### Learning process

Let $p_L$ be the empirical density (or mass) based on $L$ observations and $\hat p$ be the candidate that the machine learned. To find $w_{ij}$ and $a_i$ that minimizes the deviation of $\hat p$ from the true density $p,$ Ackley et al. (1985) chose the [Kullback-Leibler divergence](/2020/05/05/a-metric-derived-from-KL-divergence) of $p_L$ from $\hat p$ as the objective function. It is clear that if $\hat p(\mathbf x) = p_L(\mathbf x)$ then $K(\hat p\| p_L)$ so it makes sense.


$$
\begin{aligned}
K(p_n\|\hat p) 
 &= \sum_\mathbf{x} p_L(\mathbf x) \log\frac{p_L(\mathbf x)}{\hat p(\mathbf x)} \\
 &= -\sum_\mathbf{x} p_L(\mathbf x)\log \hat p(\mathbf x) + \sum_\mathbf{x} p_L(\mathbf x) \log p_L(\mathbf x) \\
 &= \mathbb E_{\{\mathbf x_\ell\}_{\ell=1}^L} \left[\log \frac1{\hat p(\mathbf x)}\right] - \mathbb E_{\{\mathbf x_\ell\}_{\ell=1}^L} \left[\log \frac1{p_L(\mathbf x)}\right]
\end{aligned}
$$


Note that the logarithm of [inverse of density can be thought of information](/2021/07/12/The-Shannon-Entropy#mjx-eqn-shannon%20entropy). Similar to how we named [mutual information](/2021/07/13/Mutual-information-and-Channel-Capacity#mutual-information), we can name this a **relative information**. 

Using the gradient descent algorithm, we get the update rule


$$
w_{ij} \leftarrow w_{ij} - \lambda \frac{\partial K}{\partial w_{ij}}\\
a_i \leftarrow a_i - \lambda \frac{\partial K}{\partial a_i}
$$


where $\lambda$ is the predefined learning rate and


$$
\begin{aligned}
-\frac{\partial K}{\partial a_i}
 &= \frac{\partial}{\partial a_i} \sum_\mathbf{x} p_L(\mathbf x)\log \hat p(\mathbf x) \\
 &= \frac{\partial}{\partial a_i} \sum_\mathbf{x} p_L(\mathbf x) (-E(\mathbf x) - \log Z) \\
 &= \sum_{\mathbf x} p_L(\mathbf x)x_i - \frac1Z \frac{\partial Z}{\partial a_i} \\
 &= \sum_{\mathbf x} p_L(\mathbf x)x_i - \sum_{\mathbf x} \hat p(\mathbf x)x_i \\
 &= \mathbb E_{\{\mathbf x_\ell\}_{\ell=1}^L} [x_i] - \mathbb E_{\hat p}[x_i].
\end{aligned}
$$


Similarly, the gradient with respect to $w_{ij}$ is 


$$
-\frac{\partial K}{\partial w_{ij}} = \mathbb E_{\{\mathbf x_\ell\}_{\ell=1}^L} [x_i x_j] - \mathbb E_{\hat p}[x_i x_j].
$$


<br>

### Implausibility

Notice that computation of gradients require summation over all possible values of $\mathbf x.$ Consider the famous MNIST dataset as an example. Suppose that each pixel has either 0 or 1 as its value. Then a single 28$\times$28 image $\mathbf x$ can have $2^{28\times28}$ different values. Summation of $2^{784}$ is implausible even for a high performant computer.



<br>

## Restricted Boltzmann Machine

It is quite discouraging that the model is implausible even for a not-so-big data. Follow up research was mainly focused on constraints makes the model plausible for data of nontrivial size while maintaining its theoretical advantages. Hinton (2002) proposed the one: the restricted Boltzmann machine (RBM).

Considera BM with hidden nodes (nodes that cannot be observed). Hinton thought of a BM as a network between layers of units. RBM restricts the ordinary Boltzmann machine by imposing a constraint that *each node within the same layer cannot have connections*.

<div style="text-align:center">
<img src="https://upload.wikimedia.org/wikipedia/commons/7/7a/Boltzmannexamplev1.png" alt="boltzmann_w_hidden.png" width="200"/>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Restricted_Boltzmann_machine.svg/440px-Restricted_Boltzmann_machine.svg.png" alt="RBM.png" width="200"/>
<br>
<em>Figure 2. (left) A Boltzmann machine with visible units (blue) and hidden units (white). (right) A restricted Boltzmann machine. (Sources: <a href="https://en.wikipedia.org/wiki/Boltzmann_machine">left</a>, <a href="https://en.wikipedia.org/wiki/Restricted_Boltzmann_machine">right</a>)</em>
</div><br>



Under this constraint, the visible unit $x_i$ can have relationship with $x_j$ only through the hidden unit $h_k.$ In this sense the hidden unit $\mathbf h$ can be interpreted as the **internal representation of $\mathbf x$**.

Now, as in the ordinary BM, we have a learned density $\hat p$ but this time it is a joint density of $(\mathbf x, \mathbf h).$


$$
\hat p(\mathbf x, \mathbf h) = \frac{e^{-E(\mathbf x, \mathbf h)}}Z,~ Z=\sum_{\mathbf x, \mathbf h} e^{-E(\mathbf x, \mathbf h)}
$$


where joint energy is defined similar to $\eqref{1}$ as well.


$$
E(\mathbf x, \mathbf h) =  \color{blue}{ -\sum_{i,j} w_{ij}x_ih_j } \color{green}{ -\sum_{i} a_ix_i } \color{green}{ -\sum_{j} b_jh_j } 
$$






[TBD]









<br>

***References***

* Hopfield. 1982. **Neural Networks and Physical Systems with Emergent Collective Computational Abilities**. Proceedings of the National Academy of Sciences of the United States of America. 79 (8): 2554-2558.
* Ackley, Hinton and Sejnowski. 1985. **A learning Algorithm for Boltzmann Machines**. Cognitive Science. 9 (1): 147-169. 
* Hinton. 2002. **Training Products of Experts by Minimizing Contrastive Divergence**. Neural Computation. 14 (8): 1771-1800. 
* Choi. 2018. **[논문으로 짚어보는 딥러닝의 맥](https://www.edwith.org/deeplearningchoi)**. 
* **The 12th KIAS CAC Summer School**, Korea Institute for Advanced Study, Republic of Korea (the talk was given by Prof. Junghyo Jo at Seoul National Univerisity).