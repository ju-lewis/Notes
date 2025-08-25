

# Substitutions

A *substitution* is a function from variables to terms.
- Notation: $\theta = \{x_1 \mapsto t_1, ..., x_n \mapsto t_n\}$

Given formula or term $E$ simultaneously replaces each occurrence of $x_i$ in $E$ by $t_i$
- Denoted by $E[\theta]$

>[!Example]
>If $E$ is $P(f(x), g(y,y,b))$, and $\theta = \{x \mapsto h(u), y \mapsto a, z \mapsto c\}$
>Then $E[\theta] = P(f(h(u), g(a, a, c))$

## Unifiers
A unifier of two expressions $s$ and $t$ is a substitution $\theta$ such that $s[\theta] = t[\theta]$
- $s$ and $t$ are *unifiable* iff there exists a unifier for $s$ and $t$.

>[!Example]
>$L(x)$ and $L(c)$ are unifiable with the substitution $\theta = \{x \mapsto c\}$

**Note:** Variables can map to other variables! (not just atoms)

We ideally want to use the most general unification.
- This means avoiding unnecessarily binding variables to terms (when they could be kept as variables)

>[!Warning]
>$x=f(x)$ is not unifiable with *finite* subtitutions.

### Solving Term Equations
- $F(s_1,...,s_n)=F(t_1,...,t_n)$
	- Replace equations with terms
- $F(s_1,...,s_n)=G(s_1,...,s_n)$
	- Halt and return failure
- $x=x$
	- Delete equation
- $t=x$ where $t$ is not a variable
	- Replace equation with $x = t$
- $x=t$ where $t$ is not $x$, but $x$ occurs in $t$
	- Halt and return failure

# Resolution for Predicate Logic

Let $P_1$ and $P_2$ be *unifiable* atomic formulas with *no variables in common*. Let $\theta$ be the unifier

Let $C_1$ and $C_2$ be disjunctive clauses:

$C_1 \cup \{P_1\}$
$C_2 \cup \{\lnot P_2\}$
---
$(C_1 \cup C_2)[\theta]$

So substitutions are performed while resolution is ongoing

>[!Example]
>$\{R(y, u), Q(x)\} \ \ \{\lnot Q(a)\}$
>Resolved: $R(y,u)$ using the substitution $x \mapsto a$
>
>**Remember**: Variables in predicate CNF are universally quantified!


We sometimes use the shorthand: $Px$ to refer to $P(x)$ where $P$ is a predicate, and $x$ is a variable.
- In refutation resolution we can use the notation: $Px,\lnot Wa$ to denote a disjunct clause between those two predicates



