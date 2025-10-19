
## Self Reference

### Proving $L_S$ is non-recognisable via self-reference

Consider the diagonalisation technique from the previous lecture.

$L_S = \{\braket{M} \ | \ M \text{ does not accept } \braket{M}\}$

Suppose $\exists \text{ TM } R \text{ s.t. } L(R) = L_S$
- $R$ accepts $\braket{R} \Rightarrow \braket{R} \in L_S \Rightarrow R \text{ does not accept} \braket{R}$
- This contradiction occurs because $L(R) = L_S$


### Proving TM acceptance is undecidable

Suppose $A_{TM}$ is decidable. $\Rightarrow \exists \text{ TM } H$ that decides $A_{TM}$ 

$H$ on $\braket{M, w}$ = accept if $M$ accepts $w$, reject otherwise.

Use $H$ to construct $D$ = on input $\braket{M}$:
- Run $H$ on $\braket{M, \braket{M}}$
- Accept if $H$ rejects
- Reject if $H$ accepts

Hence  $D$ accepts $\braket{M}$ *iff* M does not accept $\braket{M}$
- $D$ accepts $\braket{D}$ *iff* $D$ does not accept $\braket{D}$


## Reductions

Problem $A$ *reduces to* Problem $B$
- $A \leq B$
*iff*  (B is decidable $\to$ A is decidable)

Given a decider for $B$, we can construct a decider for $A$

### Examples:
- DFA equivalence $\leq$ DFA emptiness
- NFA acceptance $\leq$ DFA Acceptance


