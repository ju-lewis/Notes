

## Higher Order Programming

Benefits:
- Code reuse
- Higher level of abstraction
- A set of 'canned solutions' to frequently encountered problems


### Folds
Standard type of list *reduction*

Left fold (`foldl`): $((((I \odot X_1) \odot X_2) ...) \odot X_n)$ - builds up on the left
Right fold (`foldr`): $(X_1 \odot (X_2 \odot (... (X_n \odot I))))$ - builds up on the right
Balanced fold: $((X_1 \odot X_2) \odot (X_3 \odot X_4)) \odot ...$

This works when $\odot$ is any *binary* (two argument) function and $I$ is the *identity* value.

**Built-in folds:**
`sum`
`product`
`concat`

We can use folds with no identity element with:
```haskell
foldl1 :: (a -> a -> a) -> [a] -> a
foldr1 :: (a -> a -> a) -> [a] -> a
```
They simply error on the empty list.



We can use folds to compute the length of a list:

```haskell
const :: a -> b -> a
const x y = x

length = foldr ((+) . const 1) 0
```

Here we're using partial application of const to return 1 for every element in the list, being passed as the right argument of a partially applied summation `(+)`, so we continue to add 1 to the accumulated list length.

So the function we're applying to the list is effectively:
`(accumulated length) + const 1 x_n`
where `x_n` is the current element


**Another example**:
```haskell
map f = foldr ((:) . f) []
```


The Haskell prelude defines a function `flip` that flips the arguments of a binary function:

```haskell
[1,2] (flip (++)) [3,4] = [3,4,1,2]
```


### Foldable Types

We can fold over things other than lists

```haskell
sum (Just 7) = 7

sum Nothing = 0
```

The type declaration for `foldr` is as follows:
```haskell
foldr :: Foldable t => (a -> b -> b) -> b -> t a -> b
```


### List Comprehensions

Quicksort implementations:
```haskell
qs1 :: Ord a => [a] -> [a]
qs1 [] = []
qs1 (x:xs) = qs1 smalls ++ [x] ++ qs1 bigs
	where
		smalls = filter (<x)  xs
		bigs   = filter (>=x) xs


qs2 :: Ord a => [a] -> [a]
qs2 [] = []
qs2 (x:xs) = qs2 smalls ++ [x] ++ qs2 bigs
	where
		smalls = [l | l <- xs, l <  x]
		bigs   = [l | l <- xs, l >= x]
```

We can perform a list comprehension over multiple lists simultaneously
```haskell
[(a,b) | a <- [1,2,3], b <- [1,2,3]]
```

The expression `var <- list` is a *generator* (yields values sequentially)


Higher order programming in Haskell is *similar* to the object-oriented 'visitor' pattern
- The Haskell version is cleaner
	- We know it's not going to mutate the structure
	- We don't need to accept the result



## Libraries vs Frameworks

Libraries supply code that is intended to be called by a programmer
- User calls library code

Frameworks are intended to be the 'top layer' of the program
- The framework is *in control*
- Framework calls user code

>[!example]
>A framework for web servers would handle all communication with remote clients, and implement the event loop that waits for queries to arrive, invoking user code only to generate the responses.


### Frameworks in Haskell
```
main = framework plugin1 plugin2 plugin3

plugin1 = ...
plugin2 = ...
plugin3 = ...
```

Framework is simply a library function
- No code is generated, we're just using higher order functions!


