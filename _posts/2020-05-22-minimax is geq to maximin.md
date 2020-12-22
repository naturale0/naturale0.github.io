---
layout: post
title:  "The slowest run vs. the fastest walk: which is faster?"
date:   2020-05-22 14:46:00 +0900
author: "Sihyung Park"
categories: [decision theory]
---

Suppose there are twins with exactly same physical strength. One of them runs as slowly as he/she can, and the other walks as fast as one can. Who would be the one that crosses the finish line first?

This was the question that I encountered while killing time during some boring class activities back in the elementary school days. A crude, ill-defined question, but at the same time an interesting one worth mentioning. 

Consider the average time required to finish the race as a Bayes risk $r(\pi, \delta)$ and a decision (speed of the run/walk, between 0 and 1 for simplicity) as a concentrated prior $\pi \in (0,1)$ and an effort (whether to walk or run) as $\delta \in \\{ \text{walk}, \text{run} \\}$.

It is our objective to minimize the risk by controlling $\delta$ in various speed $\pi$. Note that if one choose to $\delta_0 = \text{run}$, with a very low speed of $\pi_0 \approx 0$, then one might be unstable and as a result $r(\pi_0, \delta_0)$ increases. Similarly it is impossible to walk with speed higher than certain amount, thus risk increases in this situation. (Yeah I know it is not so well defined context neither, but let's just skip to the interesting part)

Now let's think about this problem in decision theoretic framework. Suppose the environment decides the speed of the run ($\pi$) and the runner decides whether to walk or run ($\delta$). The runner's goal here is to minimize the risk(time), while the environment's is to maximize it.

<br>

### 1. If the environment "knows" our choise $\delta$ prior to the runner's decision.

Then it will choose the worst possible choice to the runner. That is, 

$$ \pi_{\delta} = \text{argmax}_\pi r(\pi, \delta) $$

will be its choice.

Then the runner will try to defend against the worst sinario by minimizing this as follows,

$$ \delta^* = \text{argmin}_\delta \sup_\pi r(\pi, \delta)$$

which yields the **minimax** risk:

$$ \inf_{\delta} \sup_{\pi} r(\pi, \delta) $$

$\delta^*$ here is called a **minimax rule**, while $\pi_\delta$ is called a **$\delta$-least favorable($\delta$-LF) prior**.

<br>

### 2. If the runner "knows" the environment's choise $\pi$ prior to his/her decision.

Then he/she will choose the best possible choice to reduce the time. That is, 

$$ \delta_{\pi} = \text{argmin}_\delta r(\pi, \delta) $$

will be the runner's choice.

Then the environment will try to maximize this by choosing

$$ \pi^{LF} = \text{argmax}_\pi \inf_\delta r(\pi, \delta)$$

which yields the **maximin** risk:

$$ \sup_{\pi} \inf_{\delta} r(\pi, \delta) $$

$\pi^{LF}$ here is called a **least favorable (LF) prior**.

<br>

Then here comes our theorem.

<div class="theorem" text="minimax is greather than maximin">
$$ \inf_{\delta} \sup_{\pi} r(\pi, \delta) \ge \sup_{\pi} \inf_{\delta} r(\pi, \delta) $$
</div>

<div class="proof">
It is clear by properties of $\sup$ and $\inf$.
<br>
<br>
$$
  \sup_\pi r(\pi, \delta) \ge r(\pi_0, \delta), \forall \pi_0 \in \Pi \\
  \inf_\delta \sup_\pi r(\pi, \delta) \ge \inf_\delta r(\pi_0, \delta), \forall \pi_0 \in \Pi \\
  \inf_\delta \sup_\pi r(\pi, \delta) \ge \sup_\pi \inf_\delta r(\pi, \delta)
$$
<br>
</div>

In this example, we can think of the time of race from the fastest possible walk as $\inf_{\delta} \sup_{\pi} r(\pi, \delta)$ (minimax risk), and the time of race from the slowest possible run as $\sup_{\pi} \inf_{\delta} r(\pi, \delta)$ (maximin risk).

Hence the slowest possible run is faster than the fastest walk.