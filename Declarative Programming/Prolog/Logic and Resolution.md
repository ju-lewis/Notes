
## Interpretations

- Each constant (atomic term) stands for an entity in the "domain of discourse".
- Each functor stands for a function from *n* entities to one entity in the domain of discourse
- Each predicate of arity *n* stands for a particular relationship between *n* entities

The mapping from symbols in the program to the domain of discourse is called the *interpretation*

>[!example]
>The obvious interpretation of the ground clause
>```prolog
>parent(queen_elizabeth, prince_charles)
>```
>is that Queen Elizabeth is a parent of Prince Charles


### Understanding of Predicates

1. You can think of a predicate as a function from all possible combinations of `n` terms to a truth values\
2. You can view the predicate as a set of ORDERED tuples of `n` terms. Every tuple in this set is implicitly mapped to true - while the closed world assumption renders any non-described tuples to be false.

The second understanding is a much more declarative description.


We can formally express clauses using mathematical logic notation:
$$\texttt{grandparent(A, C) :- parent(A, B), parent(B, C)}$$
becomes
$$\forall A,C : \text{grandparent(A, C)} \leftarrow \exists B \text{ : parent(A,B) } \wedge \text{ parent(B,C)}$$

For all ( $\forall$ )  is a *universal quantifier*
There exists ( $\exists$ ) is an *existential quantifier*

Facts are specific instances of rules.

Adding the reverse implication of a predicate is called the *Clark completion* of the program.


The **procedural reading** would interpret the grandparent clause as: "to show that A is a grandparent of C, it is sufficient to show that A is a parent of B and B is a parent of C".


### Finding the Semantics of a Program

You can find the semantics of a logic program P by successively applying the *immediate consequence operator*  $T_P$

$T_P$ takes a set of ground unit clauses $C$ and produces the set of ground unit clauses *implied by $C$*

This can be reapplied until the empty set is reached.


### Resolution

**Input**:
A goal $\texttt{G}$  and program $\texttt{P}$

**Output**:
An instance of $\texttt{G}$ that is a logical consequence of $\texttt{P}$ or _false_


We are trying to prove the goal `G` is true within the domain of discourse.

>[!example]
>To determine if Queen Elizabeth is Prince Harry's grandparent:
>```prolog
>?- grandparent(queen_elizabeth, prince_harry).
>```
>With the program:
>```prolog
>grandparent(X, Z) :- parent(X, Y) , parent(Y, Z).
>```
>we unify our goal with the *head* of the predicate, and apply the resulting substitution to the predicate, yielding the *resolvent*:
>```prolog
>?- parent(queen_elizabeth, Y) , parent(Y, prince_harry).
>```
>We now resolve this goal.

If a resolution fails, we backtrack to the last *choice point* (unification that failed) to continue attempting to unify the goal.

![[search-tree.png]]


Prolog uses SLD resolution (Selective Linear Definite clause Resolution). This particular type of resolution means Prolog selects the first goal to resolve, and always selects the first matching clause to pursue first. This allows the programmer to have control over the program's execution.

In this sense, Prolog executes programs with a depth-first search.


**If Prolog returns a solution with a full stop, there are no more choice points in the search tree. If there are still choice points, it will 'pretend that it failed' and returns to the choice point to unify with other clauses.**


#### Indexing

Indexing can greatly improve Prolog efficiency.
Most Prolog systems automatically index clauses according to the head's predicate name and arity such as  $\texttt{parent/2}$

Indexing changes performance, not behaviour.
