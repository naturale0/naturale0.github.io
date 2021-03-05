Usually such problem is solved by not maximizing the cumulative reward, but by minimizing the **regret function** $R$. As the name implies, $R$ is the value that represents the total loss that we had under our choices. To formally define the regret, let $\mu_i$ be the (unknown) expected reward from the $i$th arm, and $\mu_{i^*}$ be the expected reward from the (also unknown) best $i^*$th arm.


$$
\mu_i = E r_i(t) \tag{1}, \\
\mu_{i^*} \ge \mu_j,~ \forall j \ne i^*.
$$


Let $\Delta_j$ be the difference between the mean reward from the best choice and the choice $j$.


$$
\Delta_j := \mu_{i^*} - \mu_j.
$$


The regret $R$ is defines as follows:
$$
\begin{aligned}
R(T)
 &:= E \sum_{t=1}^T \left( \mu_{i^*} - r_{a(t)}(t) \right) \\
 &= \sum_{t=1}^T \Delta_{a(t)}.
\end{aligned}
$$
