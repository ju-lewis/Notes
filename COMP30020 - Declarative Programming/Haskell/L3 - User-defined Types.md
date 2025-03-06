## Type Definitions
The simplest type definition is similar to enumerated types in other languages

```haskell
-- Role can be Staff or Student
data Role = Staff | Student
```

`Role` is an arity - 0 type constructor.

The values (`Staff`, `Student`) are *data constructors*
- Data constructors must begin with a capital letter


```haskell
data Suit = Club | Diamond | Heart | Spade
data Rank = R2 | R3 | R4 | R5 | R6 | R7 | R8 | R9 | R10 | Jack | Queen | King | Ace


data Card = Card Suit Rank
```

Here, the type `Card` is like a C struct.

On the right hand side, `Card` is the *data constructor* for `Card` type
- The left `Card` is a *type*
- The right `Card` is a *data constructor*

### Printing Values

Haskell provides a *type class* called `Show` that implements the `show` function

>[!example] Recall
>Type classes are a set of types that exhibit common behaviour (e.g. share functions)

In essence, all members of the `Show` type class have access to the `show` function.


To implement `show` for our type `Rank`:
```haskell
instance Show Rank where show = showrank

-- Read: Rank is an instance of Show where the show function is showrank
```
This of course requires defining the `showrank` function.

We can get Haskell to do this automatically by using *derived* type class membership.
```haskell
data Rank = R2 | R3 | R4 | R5 | R6 | R7 | R8 |
            R9 | R10 | Jack | Queen | King | Ace
            deriving Show
```



### Eq and Ord

To be able to use `==` for a type, it must be in the `Eq` type class
To be able to order a type, it must be in the `Ord` type class

For a type to be in `Ord` it must also be in `Eq`

```haskell
data Suit = Club | Diamond | Heart | Spade
            deriving (Show, Eq, Ord)
```


### Disjunction and Conjunction

```haskell
-- Disjunction
data Suit = Club | Diamond | Heart | Spade


-- Conjunction (We have a Suit and a Rank)
data Card = Card Suit Rank
```


### Discriminated Union Types
Discriminated union types contained both disjunctions and conjunctions

The combination of disjunction and conjunction (Boolean algebra) is what makes a type system *algebraic*


```haskell
data JokerColour = Red | Black
data JCard = NormalCard Suit Rank | JokerCard JokerColour
```

When `JCard` is constructed:
- Either `NormalCard` constructor is used (`JCard` contains `Suit` and `Rank`)
- Or `JokerCard` constructor is used (`JCard` contains `JokerColour`)


### Maybe

If a value is optional, you indicate it using the `Maybe` type
```haskell
data Maybe t = Nothing | Just t
```

`Maybe` is a *polymorphic type*. 