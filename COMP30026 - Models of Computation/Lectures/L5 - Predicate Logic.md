
Propositional logic is not very expressive
- Infinite (or even large) sets are hard or impossible to express
- Complex relations and transitive verbs can't be expressed
- Relative pronouns can't be expressed adequately

>[!Example]
>"No emus fly"
>$\forall x(\text{Emu}(x) \to \lnot \text{Flies}(x))$

The expressions $\text{Emu}$ and $\text{Flies}$ encode information beyond just 'x is true' or 'x is false'
- If $x$ satisfies the $\text{Emu}$ predicate, then $x$ is an emu

# Building Blocks of Predicate Logic
1. Constants
	- e.g. $d$ represents *the* donkey
	- A specific object/single instance we are referring to
	- Use a lower case letter (near the start of the alphabet)
2. Predicates
	- e.g. $P$ for "\_ is pushing \_" or $H$ for "\_ is happy".
3. Quantifiers
	- $\forall, \exists$
4. Variables
	- Can be bound to values
	- Use a lower case letter (near the end of the alphabet)
5. Functions
	- E.g. $f,g,+$


>[!Example]
>Tina found a dog and gave it to Anne:
>$\exists x(Dog(x) \land Found(tina, x) \land Gave(tina, x, anne))$



