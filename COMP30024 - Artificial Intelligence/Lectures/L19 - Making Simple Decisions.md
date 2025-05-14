
# Combining Beliefs and Desires
Logical agents use binary goals (achieved or not)
Decision-theoretic agents assign value to outcomes
- Enables handling trade-offs and uncertainty

Probability encodes what the agent believes

We attribute *states* with utility values

## Utility
Utilities are functions $U(s)$, where $s$ is a state
- Higher utility is more preferred by the agent
- Captures agent's goal numerically

Utility functions come from multiple places:
- *Explicit design in simple cases*, e.g. adversarial games
- *Learned from experience*: Agent learns from feedback
- *Derived from preferences*: Consistent with agent's goals

A rational agent must be able to compare any two outcomes
- *Completeness*
And must be consistent in its preferences
- *Transitivity*

>[!Note]
>This is important because irrational preferences may cause agents to make contradictory or exploitable actions

**Notation**:
- $A \succ B$
	- A is preferred to B
- $A \sim B$
	- Neither A nor B are preferred
- $A \succeq B$ 
	- B is not preferred to A

![[preference-notation.png]]

>[!Info] Note
>We separate different outcomes (states) with semicolons, as we store them as tuples with their respective probability, e.g. $[p,A;q,B]$
>
>$U([p_1,S_1;p_2,S_2]) = \sum_{i=0}^n{p_i \cdot U(S_i)}$


### Decisions with Expected Utility
- Choose an action
- Each action leads to a possible outcome
- Each outcome has a probability and utility
- Compute the expected utility (EU) for each action
- Choose action with the highest EU


Act according to the **Maximising Expected Utility Principle**


## Constructing Utility Functions
Utility functions are not always obvious or easy to define
We can use the techniques:
- Direction elicitation
	- Ask user to rank or rate outcomes
- Trade-off analysis
	- Present choices that force a preference between outcomes (e.g. speed vs safety)
- Observation
	- Infer preferences from behaviour over time

**Normalised Utilities**:
- $U_{\text{best}}=1.0$
- $U_{\text{worst}}=0.0$

Examples:
- Micromorts
- Quality-adjusted life years (QALYs)
	- Useful for medical decisions involving substantial risk


### Normative vs. Descriptive Theory
**Normative**:
- Describes how a rational agent should make decisions
- Assumes consistent, utility-maxing behaviour
**Descriptive**:
- Describes how real people actually make decisions
- Often influenced by emotion, bias, framing, etc.




