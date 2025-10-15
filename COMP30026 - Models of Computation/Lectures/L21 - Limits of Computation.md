
A corollary of the Church-Turing hypothesis is that an *undecidable* problem is *uncomputable*, regardless of technology/implementation.

## 'Magic' Decider for TM Acceptance

Consider a 'magic' Turing Machine $U$ that takes as input $\braket{M}, w$ and accepts if $w \in L(M)$ and rejects if $w \not \in L(M)$
- If $M$ recognises $L$, $D$ decides $L$
	- Where $D$ is just the rule: accept if $U$ accepts, reject if $U$ rejects.

## Set Mappings
Recall definitions of *surjective* and *injective* maps

Consider mapping the set of *natural numbers* to the set of *Turing Machines*
- This seems unintuitive at first, but consider that all Python programs are *algorithms* that are represented as a string of characters, thus any algorithm we can describe in natural language (i.e. a string) can be represented as a Turing machine. This allows us to iterate all Turing Machines as a set.

Set $S$ is *countable* if it has the same size as $\mathbb{N}$
- e.g. Set of TMs and boolean strings are *countable*
- 1-1 correspondence with natural numbers

### Proving |Naturals| < |Reals| in \[0,1\]

Show that every $f: \mathbb{N} \mapsto [0,1]$ misses some real number (using *diagonalisation*)

For every $f$ ....

For every $n, f(n) \neq x$ ($f(n)$ and $x$ differ in $n$th digit.)


# Unrecognisable Languages

>[!Info] Theorem
>There is a non-recognisable language $L_D$

**Proof:**
Consider a list of all Turing machines, where $M_i$ is a Turing Machine whose encoding $\braket{M_i}$ is $i_{th}$ in string order.

|          | $\epsilon$ | $0$ | $1$ | $00$ | .... |
| -------- | ---------- | --- | --- | ---- | ---- |
| $L(M_1)$ | out        | out | out | out  |      |
| $L(M_2)$ | in         | in  | in  | in   |      |
| $L(M_3)$ | in         | out | in  | out  |      |
| $L(M_4)$ | out        | out | in  | in   |      |
....
$L_D$: in, out, out, out

We can identify a language not represented in this list by taking the entries along the main diagonal of the table and inverting them.

For every $n$, $L(M_n) \neq L_D$ (differs in the $n_{th}$ string)


>[!Example] Theorem
>If the Turing Machine acceptance problem were decidable, then the language $L_D$ would be decidable, thus there is a contradiction.


