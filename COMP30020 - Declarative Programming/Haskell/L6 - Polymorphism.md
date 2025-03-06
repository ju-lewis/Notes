
## Polymorphic Types

Defining a general tree data structure:
```haskell
data Tree k v = Leaf | Node k v (Tree k v) (Tree k v)
```

We've defined the key type to be `k` and the value type to be `v`.

`Tree` is no longer a simple type, it is a *type constructor*
	It takes a type `k` and a type `v` and maps it to an instance of a `Tree` type.


### Using Polymorphic Types

Searching a polymorphic BST:
```haskell
search_bst :: Ord k => Tree k v -> k -> Maybe v
search_bst Leaf _ = Nothing
search_bst (Node key val l r) searchKey = 
	| searchKey <  key = search_bst l searchKey
	| searchKey == key = Just val
	| searchKey >  key = search_bst r searchKey
```

**Comparing for Equality and Order**

Partial equality means we can know if they're equal, but not much else

## Data.Map

Data.Map is the built in polymorphic tree type

```haskell
import Data.Map as Map

-- Useful built-in functions
insert     :: Ord k => k -> a -> Map k a -> Map k a
Map.lookup :: Ord k => k -> Map k a -> Maybe a
(!)        :: Ord k => Map k a -> k -> a -- Infix operator
size       ::          Map k a -> Int
```

## Automatic Type Class Membership

`Show` defines a function that displays the type in the same structure as its definition
`Eq` provides exact structural equality
`Ord` provides lexicographic ordering of constructors, then arguments (e.g. `Card < Diamond`)

## Mutually Recursive Types

Datatypes can be recursive, but not *directly* recursive

In this case, it is enough that one of the types has a non-recursive alternative.


### Structural Induction

Consider a type with 1 non-recursive data constructor and 1 recursive data constructor (e.g. `Tree k v`)

A function following the structure will typically have:
- An equation for the non-recursive constructor (`Leaf`)
- An equation for the recursive constructor (`Node key val`)


#### Proof by Induction

You can view the function definition's structure as the outline of a correctness argument

- *Base case*: If $n=1$ then the applicable equation is the base case, if the first equation is correct, then function is correct for $n=1$
- *Induction step*: Assume the induction hypothesis

#### Formality

Typically software dev projects don't do formal correctness proofs
Projects using functional languages often use *informal* correctness arguments


You can perform structural induction proofs on types.
	Picking the right representation of data is incredibly important


## `let` and `where` clauses

A `let` clause (e.g. `let name = expr in mainexpr`) introduces a name for a value *to be used* in the main expression

A where clause `mainexpr where name = expr` has the same meaning, but has the definition *after* the main expression.


The one you choose depends on where you want to put the emphasis
- You can only use `where` at the *top level* of a function, you can use `let` anywhere


**Defining multiple names with clauses**

```haskell
let name1 = expr1
	name2 = expr2
in mainexpr

-- OR

mainexpr
where
	name1 = expr1
	name2 = expr2
```