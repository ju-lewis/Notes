
Logic programming is based on _predicate calculus_ and the concept of a _relation_.


# Relations
A relation specifies a relationship; for example parenthood:

## Facts
```prolog
parent(queen_elizabeth, prince_charles).
```

The above example is a **fact**.
`queen_elizabeth` and `prince_charles` are *literals*.


### Variables

Variables must begin with a capital letter.
Prolog attempts to find bindings for variables that match facts.

### Multiple Modes:
A relation can be used in many different ways to query information differently
(e.g. one could ask: "Is Y a parent of X?" or "Who is a parent of whom?")

These are different *modes* and are dictated by which arguments are bound (inputs; constants) and unbound (outputs; variables).

### Compound Queries
Prolog *goals* can be combined into more complex goals.
`,` acts as a *conjunction* operator (and)
`;` acts as a *disjunction* operator (or)

#### Example:
```prolog
?- parent(queen_elizabeth, X) , parent(X, Y).
```

Searches for all children of Queen Elizabeth who also have kids (returning grandchildren as well).
In essence, this finds the children and grandchildren of Queen Elizabeth.


## Rules
Relations can be defined using *rules* as well as *facts*

A rule has the form:
```
Head :- Body.
```

Where *Head* and *Body* are goals, with Body possibly compound. The `:-` is read "if", and the clause means that the *Head* is true if the *Body* is.

For example:
```prolog
grandparent(X,Z) :- parent(X, Y) , parent(Y, Z).
```

"X is a grandparent of Z if X is a parent of Y and Y is a parent of Z"

### Recursion

Rules can be recursive. Prolog has no looping constructs, so recursion is widely used.

```prolog
% Non-recursive:
ancestor(Anc, Desc) :- parent(Anc, Desc).

% Recursive:
ancestor(Anc, Desc) :-
	parent(Parent, Desc) ,
	ancestor(Anc, Parent).

```

### Equality

Equality is written "=" and used as an infix operator, and can be used to both to bind to variables and check for equality.

#### Examples:

This can be read the same as the previous goals: What values of X exist such that X = 7? (This is trivially when X = 7)
```prolog
?- X = 7.
X = 7.
```

This can be read as: Is the literal `a` equal to the literal `b`? which is false as all literals are different.
```prolog
?- a = b.
false.
```

Similarly, this reads: what values of X exist such that X = 7 AND X = a? Of which there are none as 7 is different to a.
```prolog
?- X = 7 , X = a.
false.
```



### Negation
Negation in Prolog is written "\\+" and used as a prefix operator. Negation has a higher (tighter) precedence than both conjunction and disjunction. 

Who are the parents of Prince William who aren't Prince Charles?
```prolog
?- parent(X, prince_william) , \+ X = prince_charles.
X = princess_diana.
```

Disequality in Prolog is written as an infix "\\=" So `X \= Y` is the same as `\+ X = Y`



### The Closed World Assumption
Prolog assumes that all true things can be derive from the program. This is not really a true assumption as it requires a *complete* program.


## Negation as Failure
Prolog executes `\+ G` by first trying to prove `G`. If this fails, then `\+ G` succeeds; if it succeeds, then `\+ G` fails. This is called *negation as failure*

`\+ G` asks if the goal `G` is *unsolvable*

#### Example:
```prolog
?- X \= queen_elizabeth.
false.
```

This may first be interpreted as:
"Are there any values of X such that X is not Queen Elizabeth?" however this is not correct according to the *negation as failure principle*. We are actually asking: "Are there no values of X where X is Queen Elizabeth?" Which is obviously false, as we have defined Queen Elizabeth in our program.


## Datalog
The fragment of Prolog discussed so far is Datalog, which generalises the behaviour of relational databases.
