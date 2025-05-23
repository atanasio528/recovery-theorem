# 1. Closed-Form for State Price Matrix

[Read the full papder (PDF)](./empirical/closed_form_ad_matrix/closed_form_for_state_price_matrix.pdf)
[Python Code](./empirical/implementation/closed_form_ad_matrix/code.ipynb)

**Summary**

We develop a closed-form solution for recovering the state price matrix (Arrow-Debreu prices) from observed European option prices across multiple tenors. Building on the framework of Ross (2015), which models the economy as a finite, time-homogeneous Markov process, we address the key limitation of prior empirical methods – numerical instability – by deriving an analytical expression using vectorization and Kronecker products. 

With the number of tenors n and the number of steps per tenor k, the maximum number of states in the economy is $N≔(n-1)k+1$. Referring to the initial state as $\omega_r$ where $1≤r≤N$, we assume that we observed spot state price vectors $\pi_t$ with time to maturities $t=1,…,nk$, which follow the induction relationship $\pi_(t+1)=Q \pi_t$ where $Q$ is the standard ratio matrix. 

The algorithm is as follows:

1. Remove the \$r\$-th element of each \$\pi\_t\$ to construct the reduced vector:

$$
\pi'_t = [\pi_t^{(r,1)}, \pi_t^{(r,r-1)}, ... , \pi_t^{(r,r+1)}]^T
$$

2. Calculate intermediate variables:

$$
B = [\pi_{k+1} - \pi_k \cdot \pi_k^{(r,r)}, ..., \pi_{nk} - \pi_{(n-1)k} \cdot \pi_{(n-1)k}^{(r,r)}] \in \mathbb{R}^{(N-1) \times N} 
$$

$$
K = [\pi'_1, \pi'2, ..., \pi'{N-1}]^T \in \mathbb{R}^{(N-1) \times (N-1)}
$$

$$
[q^{(1)}, \dots, q^{(r-1)}, q^{(r+1)}, \dots, q^{(N)}] = (K^{-1} B)^T, \quad q^{(r)} = \pi'_k
$$

3. Construct the closed form of \$Q\$ and transition state price matrix \$\Pi\$:

$$
Q = [q^{(1)}, q^{(2)}, \dots, q^{(N)}], \quad \Pi = Q^T
$$

Keywords: Recovery Theorem, Closed Form, State Price Matrix, Kronecker Product, Arrow-Debreu Prices