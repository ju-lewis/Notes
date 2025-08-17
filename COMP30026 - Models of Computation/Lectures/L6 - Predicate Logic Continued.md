

>[!Info] Note
>$\text{parent(rhonda)}$ is a *term* that likely refers to "the parent of Rhonda"
>$\text{Parent(rhonda)}$ is a *formula* that represents the proposition "Rhonda is a parent"


*Terms* are built from variables and functions:
$$t ::= x \ | \ c \ | \ f(t,...,t)$$

*Formulas* are built from predicate symbols, terms, connectives and quantifiers:
$$\varphi ::= P \ | \ P(t,...,t) | \ \bot \ | \ \top \ | \ (\lnot \varphi) \ | \ (\varphi \lor \varphi) \ | \ (\varphi \lor \varphi) \ | \ (\varphi \to \varphi) \ | \ (\forall \ x \ \varphi) \ | \ (\exists \ x \ \varphi)$$

With regard to existential quantification, $\exists$ is generalised $\lor$, and $\forall$ is generalised $\land$

>[!Example]
>Turn "*All programs output a valid number*" into a predicate logic formula.
> $$\forall x(\text{Program}(x)\to\exists y(\text{Outputs}(x, y)\land \text{Valid}(y)))$$

We can also form *parse trees* based on operator precedence to help represent the meaning of a formula.
- Tree bifurcates at binary operators

# Quantifier Scopes
The subformula attached to a quantifier is its *scope*
- A quantifier with variable $x$ *binds* $x$ within its scope.
- If a variable is not bound, it is free.

Bound variables can be renamed unless there is a clash.


>[!info] Note
>Renaming free variables changes meaning.


# Translating English to Predicate Logic
Rough guide:
1. Identify nouns, verbs, pronouns, adjectives, relative clauses
2. Assign:
	- Constant symbols to singular objects (E.g. "Rhonda")
	- Predicate symbols to verbs and adjectives (E.g. "Loves")
	- Function symbols to relative clauses (E.g. "the parent of")
	- Variables to indefinite pronouns (e.g. "someone")
3. Replicate logical structure of sentence

**Remember:** order of quantifiers is very important!!

Quantifier are often implicit in English
- e.g. "Humans are mortal" $\equiv$ "All humans are mortal"

## Meaning of a Formula

Is $\forall x \forall z (x < z \to \exists y (x < y \land y < z))$ true or false?

**It depends on how we interpret it.**
- If $x,y,z \in \mathbb{Z}$, it is false.
- If $x,y,z \in \mathbb{R}$, it is true.
- Unconditionally *true* if the universe is $\emptyset$

>[!Info] Note
>$\forall x P(X) \lor \exists y \lnot P(y)$ is *valid*
>$\forall x P(x)$ is *contingent*


# Interpretation Functions

*Non-logical symbols*: Predicate, function, and constant symbols.
*Interpretation Function*: maps every non-logical symbol to its intepretation
- Constant symbol $\mapsto$ object in $U$
- Predicate symbol $\mapsto$ relation on $U$
- Function symbol $\mapsto$ function from $U$ to $U$


## Models

A model is a universe + interpretation function

$\mathbb{Z}$ with usual $+$ is a model of $\forall x \exists y(x+y=1)$
$\mathbb{N}$ with usual $+$ is *not* a model of $\forall x \exists y(x+y=1)$


# Free Variables

The truth of $P(x)$ depends on choice of $x$

**Variable assignment:** a function $v : \text{vars} \to U$ 
- It assigns values to variables

