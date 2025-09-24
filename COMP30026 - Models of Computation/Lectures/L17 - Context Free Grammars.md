

A context-free grammar $G$ consists of:
- A finite set of terminals: $\Sigma$
- A finite set of variables $V$ (e.g. *nonterminals*)
- A finite set $R$ of production rules in the form $A \to w$
- A start variable $S$

Production rules effectively describe substitutions.

Start variables describe the "top level of parsing/substitutions"

## Notation

We can use shorthand notation for substitution rules, e.g:
$$Expr \to 0 | 1| ... | 9 | \text{ Expr Op Expr } | \text{ (Expr)}$$

If we want to generate a string from the described *context-free language*, we can just follow the production rules until we're left with only terminals

### Derivation

We say $x$ derives $z$ (or $z$ derives from $x$) and the notation $x \Rightarrow^* z$ *iff* there is a finite sequence of production rules that can be applied to obtain $z$ from $x$.

## Parse Trees

Parse trees let us visualize derivations of strings:
![[parse-tree.png]]


## Closure Properties
CFLs are closed under:
- Union
- Concatenation
- Kleene closure
- Reversal

It is *not* closed under intersection. However, if $A$ is context-free and $R$ is *regular*, then $A \cap R$ is context-free.
