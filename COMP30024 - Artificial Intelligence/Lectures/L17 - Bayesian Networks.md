
A simple, graphical notation for conditional independence assertions and hence for compact specification of full joint distributions
- Random variables are *nodes*
- Causal relationships are *arrows*
	- Arrow $\approx$ directly influences
- A conditional distribution for each node given its parents:
	- $P(X_i|Parents(X_i))$



>[!Example]
> ![[bayesian-network-example.png]]


A CPT for boolean $X$ with $k$ boolean parents has $2^k$ rows fr the combinations of parent values

Each row requires one number $p$ for $P(X_i = \text{ true})$
- The number for $X_i = \text{ false}$ is just $1-p$

If each variable has no more than $k$ parents, the complete network requires $O(n \cdot 2^k)$ numbers
- i.e. it grows linearly with $n$, vs. $O(2^n)$ for the full joint distribution


## Global Semantics

Global semantics defines the full joint distribution as the product of the local conditional distributions

$P(x_1, ..., x_n) = \prod_{i=1}^n{P(x_i|\text{parents}(X_i))}$


## Local Semantics
Each node is conditionally independent of its non-descendants given its parents

>[!Example] Alarm Example
>If an alarm goes off and John calls, we don't need to know if Mary called

**Theorem**: Local semantics $\equiv$ global semantics