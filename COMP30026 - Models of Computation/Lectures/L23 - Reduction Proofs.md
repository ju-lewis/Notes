
>[!Info] Note
>For reduction proofs, we always assume a decider for the more general problem (on the right of the $\leq$ sign)



Static code analysis
- Analyse programs without executing them
- Determine runtime errors, security vulnerabilities, specification violation, etc.


## Reducing the TM Acceptance to the Halting Problem

$\text{HALT}_{TM} = \{\braket{M, w} | \text{ M halts on input } w\}$

Then if $\text{HALT}_{TM}$ is decidable, then $L$ recognisable $\to$ $L$ decidable

## Reducing TM Acceptance to TM Emptiness

$\text{EMPTY}_{TM} = \{\braket{M} | L(M) = \emptyset\}$

**Proof**:
- Suppose $H$ decides $\text{EMPTY}_{TM}$

Construct a decider $S$ for TM acceptance

S = On input $\braket{M, w}$:
1. Construct TM $M_w$ = "On input $x$, ignore $x$ and run $M$ on $w$ and accept if $M$ accepts, and reject if $M$ rejects"
	- If $M$ accepts $w$, then $L(M_w) = \Sigma^*$, and $L(M_w) = \emptyset$ if it rejects $w$
2. Run $H$ on $M_w$
	- If $H$ accepts, reject
	- If $H$ rejects, accept

Hence TM emptiness is undecidable

## Reducing TM Emptiness to TM Equivalence

Suppose $H$ decides $\text{EQ}_{TM}$
Construct a decider $S$ for $\text{EMPTY}_{TM}$

S = On input $\braket{M}$
1. Construct TM $E$ = "On input $x$, reject."
2. Run $H$ on $\braket{M, E}$
	- If $H$ accepts, accept
	- If $H$ rejects, reject

Hence, Turing Machine emptiness is undecidable since it can be reduced to an undecidable problem.



# Closure Properties of Decidable Languages
- Complement
- Union
	- Simulate both deciders
- Intersection
	- Simulate both deciders
- Kleene closure


## Closure Properties of Recognisable Languages
- If $L$ and $L^c$ are recognisable, then $L$ is *decidable*
