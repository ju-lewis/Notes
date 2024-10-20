
A parser is a program that extracts a structure from a linear sequence of elements:

>[!example]
>Parsing `3 + 4 * 5` into a data structure representative of the order of operations


## Using an existing parser

A *Domain Specific Language* (DSL) is a small programming language with a specific purpose
- These are often embedded in existing languages


If a DSL can be parsed by extending the host language parser, it is more convenient to use
- Because it simply adds new constructs to the language


### In Prolog
`read/1` and `op/3` are very useful here

**Operator precedence**

*Precedence* - Which operators bind tightest
*Associativity* - Whether repeated infix operators associate to the right, left, or neither
*Fixity* - Is the operator infix, prefix, or postfix

```Prolog
:- op(precedence, fixity, operator)
```

Precedence is simply a number in Prolog:
- Larger number $\implies$ lower precedence

For example, goals have a precedence of 1000 


Fixity is a two or three letter symbol giving fixity and associativity
- `f` indicates the operator
- `x` indicates sub-term at *lower* precedence
- `y` indicates sub-term at the *same* precedence

operator is the operator to declare


>[!example]
>Prolog imperative for loop
>
>```Prolog
>:- op(950, fx, for).
>:- op(940, xfx, in).
>:- op(600, xfx, '..').
>:- op(1050, xfy, do).
>
>for Generator do Body :-
>	(   call(Generator),
>	    call(Body),
>	    fail
>	;   true
>	).
>```
>
>So if the `Body` (and `Generator`) call succeeds, the goal within the for loop fails, causing the `Generator` to backtrack and retrieve a new value
>



### In Haskell

Haskell operators are more simple but more limited
- You can only define infix operators

We declare infix operators with:
```haskell
associativity precedence operator
```

Where `associativity` is one of:
- `infixl` 
- `infixr`
- `infix` - non-associative

`precedence` is an integer from 1-9
- Lower numbers are *lower* (looser) precedence
- This is the *opposite* of Prolog


>[!example]
>Defining a C-like modulo operator in Haskell
>```haskell
>infixl 7 %
>
>(%) :: Integral a => a -> a -> a
>a % b = a `mod` b
>```




## Grammars

Parsing is based on a *grammar* that specifies the language to be parsed

Grammars are defined in terms of *terminals*
- These are the symbols of the language
- E.g. for an arithmetic expression: `+`, `-`, `1`, `2`, `(`, `)`, etc.
and *non-terminals*
- Specify the linguistic category (type of symbol)
- E.g. expressions, statements, or clauses

Grammars are defined by a set of rules of the form:
$$(\text{nonterminal} \cup \text{terminal})* \to (\text{nonterminal} \cup \text{terminal})*$$


>[!note]
>$\cup$ denotes the set union, $*$ is the *Kleene star* and denotes a sequence of zero or more repetitions

**Some examples**:
```
expression -> expression '+' expression
expression -> expression '*' expression
expression -> number
```

In these examples, the terminals are enclosed in quotes
- Recall terminals are what actually appear in the language programs


### Definite Clause Grammars

Prolog directly supports grammars, called *definite clause grammars* (DCG)

- Non-terminals are written using a syntax like regular Prolog goals
- Terminals are written between backquotes
- The left and right side are separated with `-->`
- Parts on the right side are separated with commas
- Empty terminal is written as `[]` or `''`

We can express the above examples as a Prolog DCG:
```prolog
expr --> expr, `+`, expr.
expr --> expr, `*`, expr.
expr --> number.
```


We can only use the above rules for determining whether the string is valid in the defined language
- Usually we want to produce a data structure (a parse tree) that represents the linguistic structure of the input

We can do this by adding arguments to our DCG (ordinary Prolog terms)

```prolog
expr(E1, E2) --> expr(E1), `+`, expr(E2).
expr(N)      --> number(N).
```



>[!note]
>Definite clause grammars map each non-terminal to a Prolog predicate that nondeterministically parses one instance of that non-terminal.
>
>This is *recursive descent parsing*


To use a grammar in Prolog, we can utilise the `phrase/2` predicate:
- In the form `phrase(nonterminal, string)`
```prolog
?- phrase (expr(Expr), '3+4*5').
```
This goal doesn't terminate due to the inability to handle *left-recursion*

### Left Recursion

A grammar rule like 
```prolog
expr(E1+E2) --> expr(E1), `+`, expr(E2).
```
is left recursive
- The first thing it does is calls itself recursively without consuming input
- This results in infinite recursion

We can rewrite our grammar to remove left-recursion:
- Rename left recursive rules to `A_rest` and remove their first non-terminal
- Add a rule for `A_rest` that matches the empty input
- Then add `A_rest` to the end of the non-left recursive rules

This is a little harder for DCGs with arguments
- You also need to transform the arguments


>[!example]
>```prolog
>expr(N) --> number(N).
>```
>
>Is transformed to:
>```prolog
>expr(E) --> number(N), expr_rest(N,E).
>```
>
>For a rule with more than 1 argument:
>
>```prolog
>expr(E1+E2) --> expr(E1), `+`, expr(E2).
>```
>
>Is transformed to:
>```prolog
>expr_rest(E1, R) --> `+`, expr(E2), expr_rest(E1+E2, R).
>```

This now terminates, however the grammar has become ambiguous
- We can't determine the associativity or precedence

This is because our definition has no description of precedence (it simply states we can parse it on both sides)


### Disambiguating a Grammar

We can ensure only the desired parse is possible by splitting the ambiguous nonterminal into separate nonterminals
- One for each precedence level

>[!example]
>```prolog
>expr(E1-E2) --> expr(E1), `-`, expr(E2).
>```
>becomes
>```prolog
>expr(E-F) --> expr(E), `-`, factor(F).
>```
>**NOTE:** this is before left-recursion removal.


So we can redefine our `expr` grammar:
```prolog
expr(E) --> factor(F), expr_rest(F,E).

% The disambiguated expr_rest definitions go here
```


![[Final DCG.png]]


### Handling Terminals
Terminals can be whatever you want
Syntax analysis is divided into *lexical analysis* (tokenising) and *parsing*

Lexical analysis uses a simpler class of grammars to group characters into tokens


In Prolog, DCGs allow us to write ordinary Prolog code in `{curly braces}`
- If the code fails, the grammar rule fails

>[!example]
>Parsing numeric literals (terminals)
>```prolog
>number(N) -->
>	[N], {'0' =< C, C =< '9'},
>	{N0 is C-'0'},
>	number_rest(N0, N).
>	
>number_rest(N0,N) -->
>	(  [C], {'0' =< C, C =< '9'}
>	-> {N1 is N0 * 10 + C - '0'},
>	   number_rest(N1, N)
>	;  {N = N0}
>	).
>```


**Note:**
DCGs can also work in reverse! parsing structured input to produce linear sequence output.


