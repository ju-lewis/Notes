
## Revisiting I/O in Haskell

Recall that we can understand monads as encapsulating a value and a description.
- The description provides extra information.


Every *complete* Haskell program must have a function `main`:
```haskell
main :: IO ()
```

In theory:
- The OS starts the program by invoking the Haskell runtime system
- The runtime system calls `main`


In actuality, the compiler and the runtime system work together to ensure each I/O operation is executed as soon as its *description* has been computed
- provided that the description is created in a context which guarantees the description will end up in the list of operation descriptions returned by `main`
- Provided that all the previous operations in that list have also been executed

>[!note]
>Here, the 'list' is the sequence of bound monadic operations


These provisions are necessary since
- You don't want to execute I/O that is not called for by the program
- You don't want to execute I/O operations out of order


### Non-immediate I/O execution

Just because you have created a description of an I/O action, does not mean that this action will eventually be executed.

Haskell programs can pass around descriptions of I/O operations without executing them directly.

>[!example]
>```haskell
>x = putStrLn "This won't print straight away!"
>```


This allows us to build up data structures of I/O actions and manipulate them.
- So we can 'execute the descriptions later' when we want to

```haskell

main :: IO ()
main = do
	-- This won't immediately execute! We're assigning the IO ()
	let x = putStrLn "abc"
	putStrLn "def"
	x
```


Haskell's purification (and labelling) of I/O operations through monadic types makes testing much easier!



### `unsafePerformIO`

Allows you to debug print without impacting the types

Should never be left in production code
- Order of output will probably be wrong due to not 'scheduling' properly with the compiler

```haskell
unsafePerformIO :: IO t -> t
```



## The State Monad

The `State` monad is useful for computations that need to 'thread information' throughout.
- Allows information to be transparently passed around (and accessed/replaced when needed)

The `State` monad abstracts the type:
```haskell
s -> (v, s)
```
where `s` is the state of the computation. It ignores the state everywhere except when explicitly required.


**Example**:
Imagine we want to perform an in-order traversal of a tree and add 1 to the first element, 2 to the second, 3 to the third, etc.


*Non-monadic approach*
We need to return the value with the tree in order to pass values in and out of the recursion stack (to track what we're adding)


We can 'hide' this threading of the integer using the `state` monad

*Monadic approach*

```haskell
incTree :: IntTree -> State Int IntTree
incTree Empty = return Empty
incTree (Node l e r) = do
	newl <- incTree l
	n <- get    -- Gets the current state (of the curr monadic computation)
	put (n+1)   -- Sets the current state (of the curr monadic computation)
	newr <- incTree r
	return (Node newl (e+n) newr)
```


### Abstracting the state operations
In the above case, we don't need the full generality of being able to update the integer state in arbitrary ways
- We just need to increment

So, we can produce a specialized version of the state monad

```haskell
type Counter = State Int

withCounter :: Int -> Counter a -> a
withCounter init f = fst (runState f init)

nextCount :: Counter Int
nextCount = do
	n <- get
	put (n+1)
	return n
```



