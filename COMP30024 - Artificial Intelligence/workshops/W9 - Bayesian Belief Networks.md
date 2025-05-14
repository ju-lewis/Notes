
# 1. Explaining Away
**1a.** 
- Burglary and Earthquake can each be described by 1 parameter (no parents)
- Alarm has 2 *binary* parents, hence the total number of combinations is $2^2$
- JohnCalls has 1 binary parent, so it has 2 parameters $2^1$
	- Same with MaryCalls

Hence the total is $1 + 1 + 4 + 2 + 2 = 10$ parameters

If we add another boolean-valued parent to alarm, $2^3$ parameters are required to model alarm given the state of the parents, so overall $2^3 + 1 + 1 = 10$  parameters are needed just to model alarm.

**1b.**
$p(X_1,...,X_n)=p(X_1|X_2,...,X_n)P(X_2,...,X_n)$
$p(X_1,...,X_n)=p(X_1|X_2,...,X_n)P(X_2|X_3,...,X_n)P(X_3,...,X_n)$
$...$
$p(X_1,...,X_n)=p(X_1|X_2,...,X_n)p(X_2|X_3,...,X_n)...p(X_{n-1}|X_n)p(X_n)$

$p(X_n)$ needs 1 parameter
$p(X_{n-1}|X_n)$ needs 2+1 parameters
$p(X_{n-2}|X_{n-1}, X_n)$ needs 4+2+1 parameters
...
Hence $p(X_1,...,X_n)$ requires $\sum_{i=1}^{n}2^{n-1}$ parameters
- This sum is essentially $O(2^{n-1})$

**1c.**
$P^*=\max_i|\text{Parents}(X_i)|$
^ Maximum number of parents for any variable in the Bayesian network

In the worst case, $\text{Parents}(X_i)=P^* \ \forall X_i \in X$

So instead of increasing by a factor of $2$ for each node, it would increase by a factor of $P^*$

**1d.**
Independent if P(Burglary|Earthquake) = P(Burglary)

# 2. Burglary or Earthquake?

# 3. Inference along a Chain

$P(X_1|X_n = \text{True}) = \frac{P(X_1,X_n = \text{True})}{P(X_n = \text{True})}$

$P(X_1,X_n=\text{True})=P(X_n=\text{True}|X_1)P(X_1)$
$P(X_1,X_n=\text{True})=P(X_n=\text{True}|X_2)P(X_2|X_1)P(X_1)$
$...$
$P(X_1,X_n=\text{True})=P(X_n=\text{True}|X_{n-1})P(X_{n-1}|X_{n-2})...P(X_2|X_1)P(X_1)$





