

## Church-Turing Thesis

"All models from algorithms can be represented as a turing machine"
- Any other reasonable model of unrestricted computation can be used (e.g. $\lambda$-calculus)



## Multi-Tape Turing Machines

The number of tapes is *fixed at compile-time*
- The first tape is the input tape
- Other tapes are work tapes


>[!Example] Theorem
>$A$ is Turing recognisable *iff* som multi-tape TM recognises $A$


A single tape turing machine can simulate a multi-tape turing machine by placing the contents of multiple tapes in "blocks" on the single tape.
- To simulate each of $M$'s steps
	- Scan entire tape to find dotted symbols
	- Scan again to update according to $M$'s $\delta$
	- Shift to add room as needed
- Accept/reject if $M$ does

## Nondeterministic Turing Machines

A *Nondeterministic TM* is similar to a Deterministic TM, except for its transition function:
- $\delta: Q \times \Gamma \to \mathscr{P}(Q \times \Gamma \times \{L, R\})$

>[!Example] Theorem
>$A$ is Turing recognisable iff some NTM recognises $A$


## Notation for Encodings and Turing Machines

If $O$ is some object (e.g. polynomial, automaton, graph, etc.), we write $\braket{O}$ to be an encoding of that object into a string. Every discrete object has a string representation

If $O_1, O_2, ..., O_k$ is a list of objects, then we write $\braket{O_1, O_2,...,O_k}$ to be an encoding of them together into a single string
- Note: typically we want a separating symbol instead of directly concatenating them.


### Acceptance Problem for DFAs

Let $A_{DFA} = \{\braket{B,w} | \ B \text{ is a DFA and } B \text{ accepts } w \}$
- **Theorem**: $A_{DFA}$ is decidable

Store both the DFA and input string on the tape and simulate the computation of $B$ on $w$. 
- Accept if it ends in an accept state, reject otherwise


### Acceptance Problem for NFAs
1. Convert NFA $B$ to equivalent DFA $B'$
2. then just simulate the DFA as before

>[!Info] Reduction
>Use conversion construction and previously constructed TM as a subroutine.
>We say that $A_{NFA}$ *reduced to* $A_{DFA}$

### Emptiness Problem for DFAs

Let $E_{DFA} = \{\braket{B} | \ B \text{ is a DFA and } L(B) = \emptyset\}$
- **Theorem**: $E_{DFA}$ is decidable

We need to check if there's a path from start to accept
- If we find some accept state from the start to an accept state then it is *not empty*
- (We can just use BFS or some other graph search)

### Equivalence Problem for DFAs

Let $EQ_{DFA} = \{\braket{A,B}| \text{A and B are DFAs and } L(A) = L(B)\}$
- **Decidable**

Two sets are the same if their symmetric difference is $\emptyset$
- We can then reduce the equivalence problem to the emptiness problem

## Simulating Context-Free Grammars

### Acceptance Problem
- **Decidable**

### Emptiness Problem
- **Decidable**

## Undecidable Problems for Context-Free Grammars

### Equivalence Problem

### Determining Ambiguity for a CFG


## Acceptance Problem for Turing Machines

Let $A_{TM} = \{\braket{M,w} | M \text{ is a TM and } M \text{ accepts } w\}$
- **Not decidable.**
- **T-recognisable**

The universality of Turing machines is an incredibly important property


