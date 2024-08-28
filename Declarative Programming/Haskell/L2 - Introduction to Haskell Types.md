

## Haskell Type System

Haskell has a *strong*, *safe*, *static* type system.


Strong means that there are no loopholes; you can't tell Haskell to consider an integer to be a pointer.

Safe means that a running program is guaranteed to never crash due to a type error.


### Basic Types
- `Bool`
- `Int`  - 32 or 64 bit
	- `Integer` for unbounded size
- `Double` (or `Float`)
- `Char`


### List
In Haskell, list is not a type; it is a *type constructor*

Given any type `t` it constructs a type for lists whose elements are all of type `t`. This type is written as `[t]` (pronounced "list of `t`")

A type constructor is a function that takes some number of types and returns a type
(Called at compile time)

**Type Constructors**
Haskell considers strings to be lists of characters, whose type is `[Char]`

Type constructors must begin with a capital letter

### GHCI REPL

**Type command**
`> :t "Hello!"` Evaluates the type of the argument
`> :l` Lists the _type of the function???_


### Type Annotation

Programmers should always explicitly declare function type signatures!

```haskell

isEmpty :: [t] -> Bool
isEmpty [] = True
isEmpty _  = False

```


**Type classes**

The numeric constant `3` belongs to `Int`, `Float`, `Double`, and `Integer` - which does Haskell say it is?
```
> :t 3
3 :: Num p => p

> :t [1, 2]
[1, 2] :: Num a => [a]
```

`Num p` means "the type `p` is a member of the type class `Num`"
If `p` is a numeric type, then `3` is of type `p`


What about the type of operators (e.g. `+`)?
```
> :t (+)
(+) :: Num a => a -> a -> a
```



### Conditional Logic


**If-then-else**

Haskell has an if-then-else construct
```haskell
iota :: Int -> [Int]
iota n = if n == 0 then [] else iota (n-1) ++ [n]
```


**Guards**

```haskell
iota n
  | n == 0 = []
  | n  > 0 = iota (n-1) ++ [n]
```



### Parametric Polymorphism

The type definition of `len` indicates it doesn't matter what the type the list contains - so long as it's consistent.
```haskell
len :: [t] -> Int
```


