
# Interpretation

An example of an interpretation function ($I$) is:
- $I(P) = \{\text{red}\}$
Which indicates the predicate $P$ only holds true for $\text{red}$


## Defining Truth in Predicate Logic

The truth of a *closed* formula depends only on the model.
- We want free variables only to define truth of a formula *compositionally*
![[compositional-truth.png]]
- Read as "the map $v$, updated to map $x$ to $d$"

In a model $M$ (with universe $U$ and interpretation function $I$) under variable assignment $v$:
- Atomic formulas: $P(t_1,...,t_n)$ is true *iff* $(v(t_1),...,v(t_n)) \in I(P)$
- Existential quantifier: $\exists x F$ is true *iff* there exists at least one $d \in U$
- Universal quantifier: $\forall x F$ is true *iff* $\lnot \exists x \ \lnot F$ is true


## Satisfaction and Consequence

We write $M, v \models F$ to mean "$F$ is true in model $M$ under variable assignment $v$".
- $F$ is *true* in $M$ *iff* we have $M, v \models F$ for all variable assignments $v$. We write $M \models F$
- $F$ semantically entails G iff every model of F is a model of G
	- We write $F \models G$

Two formulae are equivalent iff they semantically entail each other

![[predicate-validity.png]]
