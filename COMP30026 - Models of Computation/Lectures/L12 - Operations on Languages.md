
When designing an algorithm for a problem, it is often helpful to decompose the problem into simpler sub-problems. We can do something similar when designing algorithms for languages as well using the following operations:
- Complement
- Intersection
- Union
- Concatenation
- Kleene Star (AKA Kleene closure)

The last 3 are *regular operations*

Given an alphabet $\Sigma$, we define $\Sigma^*$ to be the set of all strings

>[!Example]
>When $\Sigma = \{0,1\}, \Sigma^* = \{\epsilon, 0, 1, 00, 01, 10, 11, ...\}$

A language $L$ over the alphabet $\Sigma$ is a subset of $\Sigma^*$

**Definition 1 - Complement of Language $L$:**
The complement of $L$ is defined to be the set of strings $z$ not in $L$
- I.e. $z \in L^c \text{ iff } z \not \in L$
	- Equivalently $L^c = \Sigma^* \ \textbackslash \ L$

**Definition 2 - Intersection of languages $A$ and $B$:**
The set of strings $z$ such that $z \in A \text{ and } z \in B$

**Definition 3 - Union of languages $A$ and $B$:**
Self explanatory (see above)

**Definition 4 - Concatenation of languages $A$ and $B$:**
The concatenation of $A$ and $B$ (denoted by $A \circ B$) is defined as the *set of strings* $z$ such that there exists $x \in A$ and $y \in B$ such that $z = xy$
- Essentially all possible concatenations

**Definition 5 - Kleene star of language $L$:**
The Kleene star of $L$ is defined as the set of strings consisting of:
- The empty string $\epsilon$
- $L^k$ for every positive integer $k$

>[!Note]
>$\{\epsilon\}^* = \{\epsilon\}$ and also $\emptyset^* = \{\epsilon\}$

# Closure

**Theorem 1**
Regular languages are closed under complement, intersection, union, concatenation, and Kleene star:
- If $L$ is regular, then $L^c$ and $L^*$ are also regular
- If $A$ and $B$ are regular, then so are $A \cup B$, $A \cap B$, and $A \circ B$

Moreover,
- Given a finite automaton for $L$, we can compute a finite automaton for $L^c$ and $L^*$
- Given finite automata for $A$ and $B$, we can compute a finite automata for $A \cap B$, $A \cup B$, and $A \circ B$

This proof follows by taking the finite automata for the initial languages and modifying them appropriately.

For complement this is easy: Let $M$ be the finite automaton for $L$, the finite automaton $N$ for $L^c$ is obtained by swapping accept and reject states in $M$.