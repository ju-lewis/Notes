
Resolution generalises to predicate logic
- Try to derive $\bot$
- CNF in predicate logic is *a conjunction of disjunctions of literals with all variables universally quantified*
- However, quantifiers mean that not every predicate logic formula has a CNF
- Work around by giving up on equivalence


>[!Info]
>We want to extend resolving from simple literals to resolving on atomic formulas (containing variables, constants, and function symbols)

>[!Example]
>"Every lorikeet is gorgeous" and "Coco is not gorgeous" entails "Coco is not a lorikeet"
>- $\forall x (L(x) \to G(x))$ becomes $\lnot L(x) \lor G(x)$ in CNF form
>- Combined with $\lnot G(x)$ results in $\lnot L(x)$

**Recall**: The convention with variables is that they use letters near the end of the alphabet, and constants use letters near the start.
- Also: function symbols typically use $f$ or $g$
- This is especially important when implicitly quantifying

We can 'distribute' universal quantification across conjunctions:
- $\forall x,y (P(x, y) \land Q(y)) \equiv \forall x,y, (P(x,y) \lor f(a)) \land \forall y (Q(y))$
- However, we don't write the quantifiers while performing a resolution

Since the variables are universally quantified, and we're attempting to derive a contradiction, we're finding a single instance where the predicates can't hold
- So we can make terms more similar by substituting variables for constants (since the constants are included in the universal quantification)

![[predicate-resolution.png]]


# Transforming to CNF

## Eliminating Existential Quantifiers

Consider $F: \exists x \forall y P(x,y)$
Consider $G: \forall y P(a,y)$ where $a$ is a constant symbol
- $G$ is *satisfiable* iff $F$ is
Note: For an existential quantifier *in front of* a formula


Consider $F: \forall y \exists x P(x,y)$
- We are selecting the instance of $x$ for each $y$
- E.g. for every program, we pick the number which it outputs

How do we remove the existential quantifier?
- Answer: treat $x$ as a function of the universally quantified $y$
- $\forall y P(f(y), y)$  is satisfiable iff $F$ is
Note: $f$ must be a *fresh* function symbol
- Only Skolemizing top-level existentials is examinable

## Overall Procedure
1. Eliminate $\leftrightarrow$ and $\to$
2. Push negation in (Bring to NNF)
3. Rename shadowed variables
4. Eliminate existential quantifiers (Skolemize)
5. Drop universal quantifiers (they are there implicitly)
6. Bring to CNF (using distributive laws)



