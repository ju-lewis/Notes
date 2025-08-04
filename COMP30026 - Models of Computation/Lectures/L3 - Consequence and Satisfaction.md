
>[!Note]
>$P \to Q \equiv \lnot P \lor Q$



# Semantic Consequence

$G$ is a *semantic consequence* of $F$ *if and only if* every model of $F$ is a model of $G$

For short, we write $F \models G$
$\models$ is pronounced "(semantically) entails"

>[!Example] Theorem
>Let $F$ and $G$ be formulas
>
>$F \models G \text{ if and only if } \models F \to G$
>
>As an immediate corollary
>
>$F \equiv G \text{ if and only if } \models F \leftrightarrow G$


## Formulae Types
A *tautology* is a logical formula which is always true
- $(P \lor \lnot P)$
- $P \to P$
- $\top$
A *contradiction* is a logical formula which is always false
- $Q \land \lnot Q$
- $\bot$

---
**Tautologies are valid**

Consider: "If the program works, then the program works"
- It is *true* regardless of what "program" or "works" mean.

Valid: always true
Non-valid: Sometimes false

$\models F$ is short for "F is valid"

---
**Contradictions Are Unsatisfiable**

Consider: "The application is good and the application is not good"
- It is *false* regardless of what "the application" or "good" mean

Unsatisfiable: Never true
Satisfiable: Sometimes true

---
**Most statements are contingent**

Consider: "It is currently raining"
- It is true *if and only it* it is currently raining

Contingent: Sometimes true, sometimes false


# Substitution

Replacing *all* uses of a propositional variable with a given formula

For example:
- $P \to P$ 
- Can become
- $(Q \land R) \to (Q \land R)$

Substitution preserves logical equivalence
- Denote by F\[A := B\] the result of substituting A with B in F

Example $(P \to P)[P := Q] \text{ is } (Q \to Q)$ 

>[!Example] Theorem
>$\text{If } F \equiv G \text{, then } F[P := H] \equiv G[P := H]$

## Interchange of Equivalents

If $F \equiv G$, then $F$ can freely be replaced with $G$
- A full substitution doesn't need to be performed






