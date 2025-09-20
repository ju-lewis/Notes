
Recall that the memorylessness lemma allows us to conclude that for every string $x,y$, if $q(x) = q(y)$, then $q(xz) = q(yz)$

Either $M$ accepts $xz$ and $yz$ or $M$ rejects both of them.

## Lemma
$L$ is a language
For every distinguishable pair $x$ and $y$ and every DFA $M$ that recognises $L$,
$q(x) \not = q(y)$

>[!Info] Recall
>$x$ and $y$ are *distinguishable* if concatenating a common suffix $z$ to both yields one that is rejected by $M$ and one that is accepted.

Hence for every DFA $M$ that recognises $L$, if $x,y$ are distinguishable w.r.t $L$, then $q(x) \neq q(y)$.


## Fooling Sets

>[!Example] Definition
>A set of strings $F$ is a fooling set for $L$ iff every pair $x,y \in F$ is distinguishable

### Fooling Set Lemma
$L$ is a language, $F$ is a fooling set for $L$

If $F$ has size $k$ (i.e. $|F| = k$), then every DFA that recognises $L$ has *at least* $k$ states.

Moreover, if there exists a fooling set $F_k$ with $|F_k| \geq k$ for every $k$, then $L$ is not regular.

#### Proof
Suppose $M$ is a DFA with $k-1$ states, by pigeonhole principle, $\exists x,y \in F_k$ such that $q(x) = q(y)$

So $\forall z$, $M$ accepts both $xz$ *and* $yz$ or rejects both


>[!Info] Intuitive Explanation
>If, after processing two strings $x$ and $y$, the automaton is in the same state, then *regardless* of what the suffix $z$ is, $xz$ and $yz$ must yield the same result (*see memorylessness lemma*). Hence, if appending a common suffix $z$ to $x$ and $y$ yields 2 different results (w.r.t membership of the language), these strings *must* have resulted in different states before the suffix was processed.
>
>Hence, for each distinguishable pair, there must be at least 2 states. This idea can be extrapolated as a pair-wise decomposition can be performed for all $x,y \in F_k$ to establish they must all result in different states, and thus the automaton $M$ must have at least $k$ states.

### Strategies for Fooling Sets
- Consider prefixes of strings in $L$
- Counter of $\geq$ k
- Find common distinguishing suffixes

# Nonregularity via Closure Properties
If $A, B$ are regular, then $A \cup B$ is regular.

If $A \cap B$ are *not* regular and $A$ is regular then $B$ not regular
- **Note**: any regular operation can be used, not just $\cap$.
	- E.g. $A^c$, $A \cup B$, $AB$

## Example
Let $B$ be a language of strings with an equal number of $0$s and $1$s

Let $A = 0^*1^*$ (e.g. all 0s must occur before 1s)
- $A$ is regular

$L = A \cap B$ is *not* regular (we proved this via fooling sets, as it can be described as $\{0^n1^n|n \geq 0\}$




