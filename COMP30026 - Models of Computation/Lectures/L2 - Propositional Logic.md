

# Notation
>[!Example] Well-Formed Formulae (WFF)
>
>$\varphi ::= P \ | \ \top \ | \ \bot \ | \ (\lnot \varphi) \ | \ (\varphi \land \varphi) \ | \ (\varphi \lor \varphi) \ | \ (\varphi \to \varphi)$
>

**Order of operations:**
- Unary operations (e.g. negation \[$\lnot$\]) bind stronger than all binary operations
- Conjunction and disjunction bind stronger than implication

>[!Warning]
>Formulae like $P \land Q \lor R$ are ambiguous

We can create parse trees from WFFs to intuitively represent logical structure


# Boolean Semantics

A *truth function* is a function from truth values to truth values
- Typically represented as a truth table
- E.g. inputs and outputs of a WFF given all possible assignments

A *truth assignment* is a function from propositional letters to truth values
- E.g. $v = \{P \mapsto 1, Q \mapsto 0 \}$
- $v(P) = 1, \ v(Q) = 0$

When considering formulae given some truth assignment, we ask "Is this formula *true under $v$?*"
- The shorthand for this is $v \models \varphi$ ($\varphi$ is true under $v$)

Formulae are logically equivalent iff they have equal truth values under *all assignments*
- $F \equiv G$

## Modus Ponens
A rule is *sound* if every model of the premises is a model of the conclusion
1. If P then Q
2. P is true
3. Hence, Q is true
$P \to Q, \ P \vdash Q$



