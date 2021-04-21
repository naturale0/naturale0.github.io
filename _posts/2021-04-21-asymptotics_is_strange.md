---
layout: post
title: "Asymptotics is strange..."
date:   2021-04-21 16:38:00 +0900
author: "Sihyung Park"
categories: [Nonparametric]
---

It is a useful trick to "flip" the denominator into numerator when it comes to proving asymptotic properties of errors. Here's how to do so. Consider a form

$$\frac{1}{b_0 + b_1 h + o(h)},$$

where $h \to 0$ and $b_i$'s are non-zero constants. Then

$$\begin{aligned}
&\frac{1}{b_0 + b_1 h + o(h)} \\
 &= \frac{1}{b_0\left(1 + \frac{b_1}{b_0} h + o(h)\right)} \\
 &= \frac{1}{b_0} \left(1 - \frac{b_1}{b_0} h + o(h)\right).
\end{aligned}$$

The trick is not only easy to use but easy to understand as well. Although there isn't any technically difficult part, staring at the result I could not help but say this. *Asymptotics is strange...*