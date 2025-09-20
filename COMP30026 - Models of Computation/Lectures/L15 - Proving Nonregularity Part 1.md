
**Techniques:**
Fooling sets
- Formalises "memorylessness"
- Proving the lower bound of number of states in an automata is theoretically infinite

Closure properties
- Leverage the fact that some other language is nonregular


# Fooling Sets

We want to show that for every $k > 0$, no DFA with less than $k$ states can recognise $L$

The most important aspect of finite automata definition in fooling set proofs is the *state transition function*

We define the *extended transition function* to behave like the state transition function, however it takes the next *string* to process, rather than the next symbol.
$$\delta^*(q, w)$$
where $q$ is the current state and $w$ is the next string to process
- Imagine we have processed part of a string, and we have the remaining portion of the string $w$ to process.

We perform a *prefix-suffix* decomposition on a given string in $\Sigma^*$

## Memorylessness

>[!Info] Memorylessness Lemma
> For all strings $x, y \in \Sigma^*$, if $q(x) = q(y)$ then $q(xz) = q(yz)$ for all $z \in \Sigma^*$
### Applications of the Memorylessness Lemma
If $M$ is a 1-state DFA, then $M$ either accepts every string or rejects every string.

## Distinguishable pairs and Distinguishing Suffixes
Let $L$ be a language
Let $x,y$ be strings (no necessarily in $L$)

$x,y$ are *distinguishable* if there exists $z$ such that $xz \in L$  and $yz \not \in L$


