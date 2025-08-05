
Resolution involves combining several propositional formulae in order to determine its validity
- Or just to simplify it in order to derive an atom

To show that $F$ is *valid*, refute $\lnot F$

>[!Info] Theorem
>$\models F \text{ iff } \lnot F \models \bot$

**Note: Do not cancel multiple variables at once.**
>[!Example]
> **Refute:**
> $P \lor Q, \ \lnot P \lor R, \ \lnot Q \lor R, \ S$

A resolution proof of $C_m$ from wffs $P_1, ..., P_n$ is a *string* of the form
$P_1, ..., P_n \vdash C_1, ..., C_m$ 
Where each $C_i$ is either a *copy* 

We write $``\Sigma \vdash_R F"$ to mean "there is a resolution proof of F from the set of premises $\Sigma$"
- If $\Sigma \vdash_R F \text{, then } \Sigma \models F$

# Conjunctive Normal Form (CNF)
- *Literal*: a propositional atom or its negation
- *(Disjunctive) clause*: a disjunction of literals
- *CNF*: a conjunction of disjunctive clauses
Example: $(A \lor \lnot B) \land (B \lor C \lor D) \land A$

>[!Info] Theorem
> Every propositional formula has an equivalent CNF.

## Negation Normal Form (NNF)
Only connectives are $\lnot$, $\land$, $\lor$
- $\lnot$ only in front of variables

To get NNF:
1. Eliminate $\leftrightarrow$ (Rewrite using $\to$ and $\land$)
2. Eliminate $\to$ (Rewrite using $\lor$ and $\lnot$)
3. Push $\lnot$ inward (use de Morgan's laws)
4. 

>[!Info] Theorem
> Every *unsatisfiable* set of clauses has a *resolution refutation*

## Satisfiability Algorithm
1. Convert formula into suitable form
2. Repeatedly apply resolution
	1. Derive $\bot$? Report *unsatisfiable*
	2. Can't derive anything new? Report *satisfiable*


## Simplifying CNF
**Common redundancies:**
- Duplicate variables (e.g. $P \lor P$)
- Tautologies (e.g. $P \lor \lnot P \lor Q$)
- Subsumptions (e.g. $(P \lor \lnot Q \lor R) \land (P \lor R)$)
	- If one disjunct clause is a 'subset' of another, we can use just the smaller one

## Clausal Form
Sometimes CNFs are represented as a set of literals:
- E.g $\{\{P,S,\lnot Q\}, \{P, Q\}\}$
So the disjunctions and conjunctions are implicit


## Empty Formulae
- Empty disjunction is *unsatisfiable*
- Empty conjunction is *valid*

**Explanation**:
- Disjunction is true iff at least one clause is true, which is false for an empty set
- Conjunction is true iff all clauses are true, which is inherently true for an empty set


