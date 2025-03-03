
Imperative programming is a thin layer over a computer's execution.

A functional program is more declarative, expressing a problem in pure functions 

A logic program specifies a set of equality constraints that the terms of the solution must satisfy.

A constraint logic program is more declarative still, as it allows more general constraints than just equality. 


## Constraint problem specification
- A set of variables, each variable having a known domain
- A set of constraints, with each constraints involving the variables
- An *optional* objective function
	- Maps each solution to a number, representing the *desirability* of a solution

The job of a constraint programming system is to find a *solution* (a set of assignments of variables) that satisfies all of the constraints.

The objective function allows the system to rank the solutions based on a 'score' (e.g. profit or cost)


## Types of constraint problems

### Herbrand Constraint Systems
- Variables represent terms
- Basic constraints are unifications (`term1 = term2`)
- This is the constraint domain implemented in Prolog

*Equality constraints over Herbrand terms*

**Search Strategy**
Prolog employs the "generate and test" strategy

Nondeterministic goals generate potential solutions and later goals test those solutions, imposing their respective further constraints.

>[!example]
>```prolog
>?- between(1,9,X) , 0 =:= X mod 2 , X =:= X * X mod 10.
>```
>The goals:
>1. Generates a single digit number 
>2. Checks that it is even
>3. Checks its square ends in the same digit


Constraint logic programming uses a more efficient "constrain and generate" strategy.
Constrains can be more sophisticated than simply binding to a Herbrand term, instead we can bind X to *its domain of values*

### Finite Domain (FD) Constraint Systems
- Each variable's domain has a finite number of elements

#### Solving Finite Domain Constraints

1. **Propagation**
We check whether the constraint rules out any values in the current domain of any involved variables.
If it does, we remove the value and schedule the constraints to be examined again

Propagation ends when:
- Every variable has a domain of size 1 (1 unique solution)
- Some variable has an empty domain (no solutions -> failure)
- There are more constraints to look at

2. **Labelling**
Pick a new variable
Partition its current domain (of size `n`) into `k` parts (usually `k=2`)
Recursively invoke the whole constraint solver `k` times, with each invocation restricted to the domain partition it's assigned

Generates a search tree

#### Revisiting Prolog arithmetic

CLP(FD) library (constraint logic programming over finite domains) provide replacement for lower-level arithmetic predicates (like `is/2`) allowing more multimodal usage.
![[CLPFD.png]]

Notice how the printout from `25 #= X * X` is still a goal.

This is called the **residual goal** and is the most restricted possible description of the problem. (`\/` is the symbol for disjunction)

The `label/1` predicate searches for an assignment to each variable in a list that satisfies all posted constraints

![[CLPFD Example.png]]

Sudoku is a good example of a problem that has a finite domain constraint representation.
- Values must be between 1 and 9
- No duplicates in 
This means we can make a Sudoku solver using CLP(FD)

Loading the library can be done with:
```prolog
:- use_module(library(clpfd))
```

### Boolean Satisfiability (SAT) Systems
- Variables represent booleans
- Each constraint asserts the truth of an expression constructed using logical operations (and implication)
### Linear Inequality Constraint Systems
- Variables represent *real numbers* (or integers)
- Constraints are in the form of linear inequalities ($ax+by \leq c$)
	- $x, y$ are variables and $a, b, c$ are constants

This type of solving is useful when working with continuous values and optimisation related objectives.

We can use SWI-Prolog's `library(clpr)` to solve such problems.

We can simply write out our constraints between curly braces:

>[!example]
>```prolog
>?- {250*B + 200*C =< 10000} ,
> 	{2*B =< 30} ,
> 	{75*B + 150*C =< 1200} ,
> 	{100*B + 150*C =< 1500} ,
> 	{75*C =< 700} ,
> 	{Revenue = 4*B + 6.5*C} ,
> 	maximize(Revenue).
>````

