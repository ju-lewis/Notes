
# Remaining Questions to do:
- P3.3
- 

## Propositional Logic
- Forming worded problems into propositional logic expressions
- Simplifying to CNF / RCNF / DNF / RDNF
- Proving $F \models G$ and $F \not \models G$
	- $F \models G$ can be proven using resolution (e.g. showing $F \land \lnot G \vdash \bot$)
		- It can also be proven using truth tables for simple formulae
	- $F \not \models G$ has to be proven with an example
	- Remember $F \models G \iff F \to G$


## Predicate Logic
- Conversion to CNF / RCNF
	- Skolemisation
- Definition of models (interpretation + universe)
- Resolution proof example
	- Especially an example of formatting resolution proof when typing
	- https://edstem.org/au/courses/23763/discussion/3060237


## DFAs and NFAs
- NFA -> DFA subset construction example
- Graphs displaying closure property proofs
- Non-regularity proofs
	- Fooling set proof example
	- Non-regularity proof with closure properties
- Mathematical definition (5-tuple) for NFAs and DFAs
- Regular expression syntax
	- Regular expression proofs (e.g. regular $\iff$ regex, etc..)

## CFGs and PDAs
- Creating CFG for language description
- CFG to PDA algorithm
	- Also CFG to PDA examples (without algorithm)
- Mathematical definition for PDAs


## Turing Machines
- Formal definition
- When diagramming, reject states aren't explicitly shown, they are implicitly reached from missing transitions
- Known undecidable problems and their 'arguments' (and how to reduce to them)
	- CFG problems
	- Turing machine problems
- Proving *unrecognisability* using the diagonalisation technique
	- Also include a quick summary of set mapping content
- Brief mention of multi-tape turing machines
