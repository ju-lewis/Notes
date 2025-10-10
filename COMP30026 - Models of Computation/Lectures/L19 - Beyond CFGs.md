

>[!Info]
>Note, there are some context-free grammars that cannot be recognised by *deterministic* pushdown automata (they require a degree of non-determinism).


The language $\{0^n1^n2^n \ | \ n \geq 0 \}$ cannot be recognised by a context free grammar, as once you have verified the constraints for $0$ and $1$, there is no way to remember the values to verify the constraints for the $2$'s in the input string.

# Turing Machines

Instead of having *unbounded* memory with *restricted* access (e.g. a stack), we have a tape with *random access* that can *read and write*

**Important Features**
1. Head can read and write
2. Head is two way
3. Tape is infinite (to the right)
4. Infinitely many blanks " " follow input
5. Can accept or reject at *any time*
	- Computation halts whenever the head reaches an accept/reject state


>[!Example] Example - Recognising $a^nb^nc^n$
>
>1. Scan right until " " while checking if input is in $a^*b^*c^*$, reject if not.
>2. Return head to left end.
>3. Scan right, crossing off a single $a$, $b$, $c$
>4. If the last one of each symbol, accept.
>5. If the last symbol of some but not all, reject.
>6. Repeat from step 3 until an accept/reject condition is met.
>

## Formal Definition
- $\Sigma$ - Input alphabet
- $\Gamma$ - Tape alphabet $\Sigma \subseteq \Gamma$
- $q_0$ - Initial state
- $q_{acc}$ - Accept state
- $q_{rej}$ - Reject state
- $\delta$ - $Q \times \Gamma \to Q \times \Gamma \times \{L,R\}$
	- *Note:* L and R refer to directions for moving the head.

On an input $w$ a TM $M$ may halt (enter $q_{acc}$ or $q_{rej}$) or $M$ may run forever ("loop").
- So there are 3 possible outcomes when account for infinite looping

**However**, the language of the machine is stilled strictly defined as the set of strings *accepted* by the machine.

>[!Info] Theorem
>A Turing Machine $M$ is a *decider* if it halts for all inputs.

## Graphical Notation:

![[turing-machine-notation.png]]
- Character on the left of the arrow denotes parsing something from the input (i.e. it gates the transition)
- *If* the tape is to be mutated at the location of the head, another character in the language is written after the right arrow
- Finally, the direction to move the head in is written at the end (either $L$ or $R$)


## Configuration

The configuration of a TM is defined by a "snapshot of its execution at a point in time":
- Current state
- Current state of the tape
- Current location of the tape head


If applying configuration $\delta$ to config $C$ yields config $C'$, we write $C \Rightarrow C'$

>[!Example]
>$u\textbf{q}bv \Rightarrow uc\textbf{t}v$ if $\delta(q,b) = (t,c,R)$


## TM Recognisers and Deciders

Let $M$ be a TM. Then $L(M) = \{w | M \text{accepts} w\}$

Say that $M$ recognises A if A = L(M)
- A is Turing-recognisable if $A = L(M)$ for some TM $M$

Say that $M$ decides $A$ if $A=L(M)$ and $M$ is a decider.


