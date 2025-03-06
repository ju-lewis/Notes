

>[!note]
>A *monad* is a type constructor that represents a computation. These computations can then be composed to create other computations, and so on.


The power of monads lies in the programmer's ability to determine *how* the computations are composed.

**All monads are functors and applicative functors**

A monad `M` is a type constructor that supports 2 operations:

1. Bind (a sequencing operation) - denoted `>>=`
	- `M a -> (a -> M b) -> M b`
2. An identity operation - denoted `return`(wraps a type into a Monadic type)
	- `a -> M a`

Bind can be thought of as analogous to function composition with the `.` operator, but for computations concerning Monads


Monads in Haskell (using bind) can be described as programmable semicolons.




Think of the type `M a` is a computation that produces an `a`, and possibly carries extra info
- E.g. the value could be `Nothing` in the context of `Maybe a`, or an error might have occurred


Once you have a 'wrapped' value, you can use the sequencing operation to perform operations on it. `>>=` will unwrap the first argument and invoke a function given as a second argument.
- Returns a wrapped result


**Defining Rust's `Result` type:**
```haskell
data Result t = Ok t | Err

-- Wrapping the value
return r = Ok r

-- Defining how sequencing should be performed
(Ok x) >>= f = f x
Err >>= _ = Err
```


## Using Monads to Simplify Code

Say we wanted to write a function that computes the square root of the head of a list of `Int`

```haskell
-- Assume appropriate definitions for the following functions
maybeHead :: [a] -> Maybe a
maybeSqrt :: Int -> Maybe Double


-- Approach 1 - without using Monadic computation
maybeSqrtOfHead :: [Int] -> Maybe Double
maybeSqrtOfHead x = 
	case maybeHead x of
		Just h -> maybeSqrt h
		Nothing -> Nothing


-- Approach 2 - binding Monad computations
maybeSqrtofHead x = 
	maybeHead x >>= maybeSqrt

```



## I/O Actions in Haskell

Haskell has an `IO` type constructor
A function that returns a value of type `IO t` will return a value of type `t`, but also does input/output functions

**Examples**
Input:
`getChar :: IO Char`
`getLine :: IO String`

Output:
`putChar :: Char -> IO ()`
`putStr :: String -> IO ()`


>[!note]
>`()` is the *unit type* in Haskell. It is a 0-tuple.




### Operations of the I/O monad

The *identity operation* simply wraps a value in the `IO` monadic type without performing any input/output functionality


The *sequencing operation* `f >>= g`:
1. Calls `f`, which may do I/O, and returns value `rf`
2. Calls `g rf` Which also may do I/O
3. Returns `IO rg`

Note that any of `rf` or `rg` can be unit types.


>[!example]
>We can define `putStrLn` like this:
>
>```haskell
>myPutStrLn = putStr >>= (\_ -> putChar '\n')
>```
>
>This point-free definition will print a string with `putStr`, returning an `IO ()`. It then uses a lambda function to ignore the result of the `putStr` call, and prints a newline character.



## `Do` Notation

We can see how chaining together lots of anonymous functions that ignore returned values from I/O functions gets very verbose and ugly for larger programs.

`Do` notation lets us simplify this.

```haskell
myPutStrLn = do
	putStr
	putChar '\n'
```

Each element of a `do` block can be:
- An I/O action that returns an ignored value
- An I/O action whose return value if bound to a variable
- Bind a variable to a non-monadic value


```haskell
greet :: IO ()
greet = do
	putStr "Hi! What's your name? "
	name <- getLine
	purStr "Where are you from? "
	town <- getLine
	let msg = "Welcome, " ++ name ++ " from " ++ town
	putStrLn msg
```


**Note:**
We can use the `$` infix operator to ensure the precedence of operands

```haskell
putStrLn "Hello " ++ "there" -- DOESN'T COMPILE!!
putStrLn ("Hello " ++ "there") -- This works!
putStrLn $ "Hello " ++ "there" -- This works too!
```

This works as the `$` has very low precedence, forcing the concatenation to be performed first.


### `return` keyword

If you have an I/O function that returns the value from a non-I/O call, e.g. a function that reads in a string and then computes its length, you need to explicitly wrap the value in an `IO` monad (with the identity operator `return`).

```haskell
readlen :: IO Int
readlen = do
	str <- getLine
	return (length str)
```




