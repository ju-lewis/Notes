
## Application Binary Interfaces

A *platform* is a combination of an instruction set architecture (ISA) and an operating system, e.g. x86/Windows

Each platform typically has an *application binary interface*, or ABI, which dictates things like:
- Where the callers of functions should put parameters
- Where the callee should put the results

This is how languages were traditionally interfaced, as they would have compatible compiled binaries

### Beyond ABIs
The application binary interface model doesn't work for more advanced languages
- Non-determinism in Prolog
- Laziness in Haskell
- V-Tables in C++


## Applications for Foreign Function Interfaces


### Boolean Functions

Consider the case where we want to determine the satisfiability of boolean expression, in essence - are there any variable bindings such that a given expression is true?
- This problem is NP-hard


#### Binary Decision Diagrams

BDDs are decision diagrams based on *if-then-else* (ite) nodes, where each node is labeled by a boolean variable and each leaf is a truth value

With a *truth assignment* for each variable, the value of the formula can be determined by traversing from the root, following *then* branch for true variables and *else* branch for false variables.

![[BDD.png]]


We can represent a BDD in Haskell like so:
```haskell
data BDD label = BTrue | BFalse | Ite label (BDD label) (BDD label)
```

The meaning of a BDD is given by:
*meaning* `BTrue` = true
*meaning* `BFalse` = false
*meaning* (`Ite v t e`) = (v AND *meaning* t) OR (not v AND meaning e)
- Either *then* branch must be true or *else* branch must be false

#### ROBDDs
Reduced Ordered Binary Decision Diagrams are BDDs where: 
- labels are in increasing order from root to leaf
- no node has two identical children
- No two distinct nodes have the same semantics

![[ROBDD.png]]

ROBDD algorithms traverse DAGs, and often meet the same subgraphs repeatedly. They greatly benefit from *caching*

Caching requires efficiently recognising when a node is seen again
- Haskell doesn't have a concept of **object identity**, so it can't distinguish between duplicate sub-trees and internal links to the same sub-tree


>[!note] Implementing ROBDDs in Haskell
>
>Building a new ROBDD node `ite(v, thn, els)` must ensure that:
>- The two children of every node are different
>	- Achieved by checking if `thn = els`, if so, returning `thn`
>- For any boolean formula, there is only one ROBDD node with that semantics
>	- Achieved by *structural hashing* (AKA *hash-consing*)
>	- Maintaining a hash table of past calls `ite(v, thn, els)` and their results

Now we can easily determine boolean satisfiability by checking it doesn't lead to false in the ROBDD, and equality can be determined by equating ROBDDs.


Note that we haven't cheated the NP-Completeness, we've just shifted computation cost to building the data structure.


## Interfacing C to Haskell

We can interface to a C function with a declaration in the form:
```haskell
foreign import ccall "C Name" {- Haskell name -} :: {- Haskell type -}
```

C primitives convert to and from natural Haskell types:
`C int <-> Haskell Int`

We want to treat ROBDDs as an *opaque type*
- A type we cannot peer inside, we can only pass it around foreign functions

The type `Word` represents a word of memory (pointer), however it is not opaque.


Declaring `type BoolFn = Word` would not make `boolFn` opaque; it's just an alias
We can use the `newtype` keyword to declare types with only one constructor
```haskell
newtype BoolFn = BoolFn Word deriving Eq
```

We can now use our opaque type in the FFI:

```haskell
foreign import ccal "is_true" isTrue :: BoolFn->Bool
-- etc.
```


To load our C functions into a Haskell environment, we first compile the C program:
```bash
gcc -c -Wall robdd.c
ghci robdd.o # We can load the object file!
```


## Interfacing C to Prolog

```prolog
:- use_foreign_library(swi_robdd)
```
This will load a compiled C library file that links the code in `swi_robdd.c` which forms the interface to prolog, and the `robdd.c` file


```bash
swipl-ld -shared -o swi_robdd swi_robdd.c robdd.c
```


A C function that implements a Prolog predicate needs to convert between Prolog terms and C data structures. This is called *marshalling* data


To prevent Prolog from confusing an ROBDD (pointer) from a number, we wrap the address in a `boolfn/1` term, like we did in Haskell.

```prolog
% conjoin(+BFn1, +BFn2, -BFn)
% BFn is the conjunction of BFn1 and BFn2

conjoin(boolfn(F), boolfn(G), boolfn(FG)) :-
	boolfn_conjoin(F, G, FG).
```

We can implement a type of pretty-printing by adding a clause for `user:portray/1`


## Impedance Mismatch
Declarative languages typically use very different representations even for similar data
- Interfaces are usually low level as a result


### Benefits of Declarative Programming
- Less bug-prone
- Easier conceptualisation of logical problems
- Easier maintainability
### Benefits of Imperative Languages
- More tooling
- More programmers who know the languages
- Typically faster



