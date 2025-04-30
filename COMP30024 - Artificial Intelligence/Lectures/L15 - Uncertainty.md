
>[!Example]
>Let action $A_t$ = leave for the airport $t$ minutes before flight.
>Will $A_t$ get me there on time?
>
>Problems:
>1. Partial observability (road state, other drivers' plans, etc.)
>2. Noisy sensors (radio traffic report)
>3. Uncertainty in action outcomes (flat tyre, etc.) 
>4. Immense complexity of modelling and predicting traffic

## Methods for Handling Uncertainty

**Nonmonotonic logic**
- Assume my car does not have a flat tyre
- Assume $A_{25}$ works unless contradicted by evidence

Issues:
- What assumptions are reasonable?
- How to handle contradiction?


**Rules with confidence factors**
- $A_{25} \rightarrow_{0.3}$ get there on time
- However, consider the example:
	- $\text{Sprinkler} \rightarrow_{0.99}$ wet grass
	- $\text{WetGrass} \rightarrow_{0.7} \text{Rain}$
	- Does sprinkler $\implies$ rain ???

**Probability Theory** is the best method.


# Probability

Probabilistic assertions *summarise* effects of:
- *Laziness:* failure to enumerate exceptions, qualifications, etc.
- *Ignorance:* lack of relevant facts, initial conditions, etc.

Bayesian (subjective) probability:
- Probabilities relate probabilities to one's own state of knowledge

These are *not* claims of some probabilistic tendency in the current situation

>[!Example]
>$P(A_{25}|\text{ Observations })   = 0.04$
>$P(A_{90}|\text{ Observations })   = 0.70$
>$P(A_{120}|\text{ Observations })  = 0.98$
>$P(A_{1440}|\text{ Observations }) = 0.99999$


## Propositions
Think of a proposition as the event (set of sample points) where the proposition is true
- i.e. boolean conditions
- Indicator random variables

Given Boolean random variables $A$ and $B$:
- event $a$ = set of sample points where $A(\omega)=\text{true}$
- event $\neg a$ = set of sample points where $A(\omega) = \text{false}$
- event $a \wedge b$ = points where $A(\omega) = \text{true}$ and $B(\omega) = \text{true}$



### Syntax for Propositions

**Propositional** (or boolean) random variables
**Discrete*** random variables
- Does a variable take a certain value out of a set?
**Continuous** random variables
- Does a variable take a value within a range from an uncountable set?
**Arbitrary combinations**


Note: we use the bold **P** notation to indicate the entire probability distribution for the random variable.


