

# Factoring

Consider clause $C$ with unifiable $A_1, A_2 \in C$
Given $\text{mgu } \theta$, add the clause $c[\theta]$

>[!Example]
>1. $\{D(f(y), y), \lnot P(x), D(x,y), \lnot P(z)\}$
>2. $\{D(f(y), y), \lnot P(f(y)), \lnot P(z)\}$
>3. $\{D(f(y), y), \lnot P(f(y))\}$


## The Need for Factoring

Consider the disjunct clauses:
$\{P(x), P(y)\}$ and $\{\lnot P(u), \lnot P(v)\}$

We can first simplify (factor) to:
$\{P(x)\}$ and $\{\lnot P(u)\}$

Which can then be resolved to $\bot$

## The Resolution Method
Start with collection $\Sigma$ of clauses
While $\bot \not \in \Sigma$ do:
- Add to $\Sigma$ a factor of some $C \in \Sigma$
- *OR* a resolvent of some $C_1, C_2 \in \Sigma$


# The Power of Resolution

>[!Info] Theorem
>$\Sigma$ is unsatisfiable iff the resolution method can add $\bot$ after a *finite* number of steps.

We say that such a resolution is *sound* and *refutation-complete*

Not a *decision procedure*: may not terminate on satisfiable formulas.

Indeed, no such procedure can exist for predicate logic.
- Validity/unsatisfiability are *semi-decidable* properties

# Horn Clauses and Prolog

A horn clause is a clause with *at most* one positive literal.
- E.g. $\{\lnot T(z), \lnot D(y), \lnot E(y,z), M(z)\}$

We can rewrite this as the implication:
$(T(z) \land D(y) \land E(y,z)) \to M(z)$

And express it in Prolog as:
```prolog
miserable(Z) :- tadpole(Z), deepwaterfish(Y), eats(Y,Z).
```

## Horn Clauses and Search

For propositional horn clauses, satisfiability can be decided in linear time
- For logic programs,. the restriction to horn clauses simplifies the search problem (but does not remove it)

![[horn-clause-satisfiability.png]]


# Equality in Automated Reasoning

Add a new predicate symbol $eq(X,Y)$ and axiomatize it
- Define reflexivity, symmetry, transitivity, congruence
![[automated-reasoning.png]]
