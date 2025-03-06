
## Primitives (Atomic Terms):
- Integers
- Floating point numbers
- Atoms
	- Begin with a lower case letter and follows with letters, digits, and underscores
		- e.g. `banana`, `queen_elizabeth`
	- Technically functors with 0 arguments

## Variable Terms:
- Dynamically typed
- Can be bound to any other type of term
- Begin with lowercase letter or underscore (if anonymity is desired)

## Compound Terms:
- Analogous to C structs
- Declaration syntax:
	- `functor(arguments)`
	- Example: `card(clubs, 3)`
- Compound terms can have variable-valued arguments
	- These variables are bound through *unification*
	- This is the process of trying to find consistent bindings for all contained variables.

#### Predicates are instances of functors that we use to express facts.


An example of a small tree with:
- The value `1` at the root
- An empty left branch
- A `2` in the right branch

Could be expressed as:
```prolog
node(leaf, 1 node(leaf, 2, leaf)).
```

**Remember Prolog is dynamically typed!**
Prolog has infix notation for specific functors.

## Lists:
The empty list  `[]` is an atomic term 
All other lists are compound terms.

#### Variables are also terms in Prolog.
Because the arguments of a compound term can be any terms - variables can be in terms.


## Ground vs Nonground terms
A term is *ground* if it contains no variables, and is nonground if it contains at least 1.
A nonground term becomes ground when it is bound to an atomic term.


### Substitutions
A substitution is a mapping from variables to atomic terms.

An example of applying a substitution to a nonground term is:
`node(X1, X2, X3)` becoming `node(leaf, 1, leaf)`
The ground result of this transformation is an *instance* of the nonground version.

Nonground terms have an infinite number of *instances* representing the infinite possible substitutions.



## Unification
The term that results from applying a substitution $\theta$ to a term $t$ is denoted $t\theta$.

A substitution $\theta$ *unifies* two terms $t$ and $u$ if $t\theta = u\theta$.

**Example:**
Given terms `f(X, b)` and `f(a, Y)`
The substitution: $\{ {\texttt{X} \mapsto \texttt{a}} \}$ results in two terms: `f(a, b)` and `f(a, Y)`hence is not unifying
The substitutions: $\{ \texttt{X} \mapsto \texttt{a}, \texttt{Y} \mapsto \texttt{b} \}$ result in 2 instances of `f(a, b)`, so it is *unifying*.


When you 'query' Prolog, it attempts to unify your goal with the predicates in your program. If it can, it tells you the substitutions used to do it.


#### When coding in Prolog, think of checking a result is correct instead of computing it.


## Arithmetic

Writing `6 * 7` is just an infix expression for `*(6, 7)`, hence Prolog simply unifies this to `6*7`.

The built in predicate for evaluating arithmetic expressions is `is/2`:
`X is 6*7` is an infix shorthand for `is(X, 6*7)` where `6*7` is evaluated.
 

**Built in arithmetic operators:**
- `+,-,*`
- `/` division (may return a float)
- `//` integer division (floor)
- `mod` 
- `-` Unary minus (negation)
- `integer` `float` coercions
- `< =<`
- `> >=`
- `=:= =\=` equal, not equal (numbers only)

