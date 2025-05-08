
# Constructing Bayesian Networks

Need a method such that a series of locally testable assertions of conditional independence guarantees the required global semantics.

1. Choose an ordering of variables $X_1,...,X_N$
2. For $i=1$ to $n$:
	- Add $X_i$ to the network
	- Select parents from $X_1,...,X_{i-1}$ such that:
		- $P(X_i|\text{Parents}(X_i)) = P(X_i|X_1,...,X_{i-1})$A
		- Because $X_i$ is independent to all other variables in $X_1,...,X_{i-1}$ 
The choice of parents guarantees the global semantics

The ordering is important! We may end up with non optimal graph constructions with bad ordering
- Defining conditional independence is hard in non-causal directions

>[!Info] Solution
>We typically order the variables from causes $\rightarrow$ effects

## Inference Tasks
**Simple queries**: Computing posterior probabilities
**Conjunctive Queries**: Probability of two random variables being true
**Value of information**: Which evidence to seek next?
**Sensitivity Analysis**: Which probability values are most critical?
**Explanation**: Why did this outcome occur? / Why is this cause probable?


### Inference by Enumeration

Slightly intelligent way to *sum out variables* from the joint distribution without constructing its explicit representation

Recursive depth-first enumeration:
- $O(n)$ space
- $O(d^n)$ time

### Inference by Variable Elimination

**Pictured: Inference by enumeration**
![[inference-by-enumeration.png]]
There are clearly inefficient repeated computations when summing over hidden variables

**Variable elimination** involves carrying out a sum 'left-to-right', storing immediate results (factors) to avoid recomputation
- Dynamic programming approach


