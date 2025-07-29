
>[!Example] Fundamental Logic Notation
>$\land$ - Conjunction
>$\lor$ - Disjunction
>$\to$ - Implication
>$\neg$ - Negation

**Logical Sudoku Solver**
Boolean $x_{ijd}$ means field $i,j$ has digit $d$
- Top left field is $1,1$
- Bottom left field is $9,9$

We can compactly represent the requirements of the sudoku problem using a series of boolean variables and several logical constraints:
$\land\{\text{at-least-one}(\{x_{ijd}|d \in D\})|i,j\in D\} \land \land\{\text{at-most-one}(\{x_{ijd}|d \in D\})|i,j\in D\}$

An efficient logical solver can iterate over solutions using these constraints



