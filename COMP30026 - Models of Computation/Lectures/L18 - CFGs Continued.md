
## Ambiguity

In general, there are often multiple possible derivations of a CFG to reach a given string.

This means multiple different parse trees can be produced for a single string.

Ideally we want to produce unambiguous grammars


# Pushdown Automata

DFAs and NFAs have limited memory (current state only)

We can augment NFAs by providing an unlimited *stack* (FIFO access)
- This provides more memory and the ability to recognise more complex languages

>[!Example]
>A DFA cannot recognise $\{a^nb^n | n \geq 0\}$ because of the lack of memory (no way to verify the number of $b$s matches the number of $a$s)
>
>But a PDA can recognise it.
>
>For each $a$ encountered, push it to the stack. For each $b$ encountered, pop it from the stack.
>
>![[pushdown-automaton.png]]
>
>**Note**:
>- The transition annotations now have *2* components:
>	- The first describes the character consumed from the input string
>	- The second describes the operation to the stack
>		- The character to the *left* of the arrow is what we *pop* from the stack
>		- The character to the *right* is what we *push* onto the stack.


In PDAs, if we want to check if the stack is empty, we typically push a `$` symbol to the stack at the start of processing and check if we can pop it at the end
- There is no way to directly check if the stack is empty without adding this special terminating character.


A pushdown automaton is a 6-tuple $(Q, \Sigma, \Gamma, \delta, q_0, F)$ where
- $\Gamma$ is the *stack alphabet*
- $\delta : Q \times \Sigma_\epsilon \times \Gamma_\epsilon \to \mathscr{P}(Q \times \Gamma_\epsilon)$ is the *transition function*
(Other elements of the 6-tuple are the same as DFAs and NFAs)


>[!Info] Note
> There is no requirement that $s_n = \epsilon$, so the stack may be non-empty when the machine stops.
> 
> Also, an empty stack *cannot* be popped.


![[pda-example-2.png]]



>[!Cite] Theorem
>A language is context-free if and only if it is recognised by a PDA.


## Regular Grammars
If we restrict the kind of rules allowed in CFGs, so they must be either of form:
- $A \to w$ OR $A \to w B$

With $w \in \Sigma^*$ and $A,B \in V$, then we have *regular grammars*.
- These generate exactly the regular languages.



