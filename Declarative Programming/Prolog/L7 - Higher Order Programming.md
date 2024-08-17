
Prolog is a *homoiconic* language - Prolog programs can manipulate Prolog programs as data.

An example of this is the built-in predicate `clause(+Head, -Body)` which is true if `Head` can unify with the head of a clause and `Body` unifies with the corresponding body.



Interestingly, a call to `clause(append(X, Y, Z), Body)` fails.
This happens because 'built in' predicates aren't actually built-in, rather they're *autoloaded*

Since we called `clause/2` before `append/3` was autoloaded, it cannot be found. We can explicitly load `append/3` as follows:
```prolog
use_module(library(lists), [append/3]).
```

This results in somewhat impure behaviour as all predicates should be independent.


The `clause/2` predicate makes it very easy to write an interpreter in Prolog:
```prolog
interp(Goal) :-
	( Goal = true
	-> true
	; Goal = (G1, G2)
	-> interp(G1) , interp(G2)
	; clause(Goal, Body),
	  interp(Body)
	).
```

## Higher Order Programming

The `call/1` predicate executes a term as a goal, capitalising on Prolog's homoiconicity

### Currying

It is often useful to provide a goal while omitting some arguments (which are supplied when the goal is called)

To support this, many implementations of Prolog support *higher arity* implementations of `call` so you can 'bundle' arguments with it.


An example of writing higher order predicates using `call/n` is using `maplist/3` to apply a predicate elementwise to the elements of 2 lists

![[higher order predicate.png]]

### Storing Solutions
`setof(+Template, :Goal, -List)` binds `List` to a sorted list of all distinct instances of `Template` satisfying `Goal`

**Note**: the mode `:` is a special case of `+` indicating a meta-argument

`Template` can be any term, usually containing some of the variables in `Goal`

>[!example]
>```prolog
>setof(P-C, parent(P, C), List).
>```

If `Goal` contains variables not appearing in `Template`, `setof` will return distinct results for all possible bindings (supports backtracking for the 'nested' goal).


To avoid this non-deterministic behaviour (i.e. if we want to simply report all of the parents in the DB without needing to backtrack over unbound children) we can use **existential quantification** with the caret (`^`) operator:

```prolog
?- setof(P, C^parent(P, C), Parents).
```

will simply return all of the parents as a list, as opposed to

```prolog
?- setof(P, parent(P, C), Parents).
```

Which will backtrack over all possible bindings for `C`.


There is a different predicate for reporting all solutions *without* sorting them or removing duplicates: `bagof/3`

This predicate is *not purely logical* as the order of solutions and number of solutions are not related to the pure logic of the program.

Use cases:
- Debugging
- Improving efficiency by removing sorting

### Comparing Terms
**All** Prolog terms can be compared for ordering using:
`@<`, `@=<`, `@>`, `@>=`

Using the ordering:

Variables < Numbers < Atoms < Compound Terms


Within these classes, terms are ordered as expected.

### Sorting
`sort/2` sorts a list, removing duplicates as well
`msort/2` sorts a list without removing duplicates
`keysort/2` stably sorts lists of `X-Y` terms by comparing only `X` components



### Determining Term Types
`integer(@Term)` succeeds if `Term` is bound to an integer at call time
`float(@Term)`
`number(@Term)`
`atom(@Term)`
`compound(@Term)`

**Remember that `@` implies the predicate doesn't instantiate the argument**


We can check if terms are bound:

`var/1` holds for unbound arguments
`nonvar/1` holds for any term *other* than an unbound variable

Using type testing we can combine multiple predicates into a single predicate that handles different types or different modes. This allows us to make more predicates tail-recursive


### Input/Output
Prolog's input/output is obviously not pure

The `op/3` predicate allows for user defined operators

>[!example]
>```prolog
>op(800, xfy, wibble).
>```

`800` is the priority
`xfy` denotes that it's an infix operator
`wibble` is just the name

Prolog has built-in predicates for reading and writing arbitrary Prolog terms.

>[!example]
>```prolog
>?- read(X), write(X), call(X).
>|: This wibble That.
>_17214 wibble _17216
>```

See how the 'input' can be bound to variables



