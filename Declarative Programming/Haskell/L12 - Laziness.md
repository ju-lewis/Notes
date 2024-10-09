

In a programming language that uses *eager evaluation*, each expression is evaluated as soon as it gets bound to a variable.

In a programming language with *lazy evaluation*, an expression is not evaluated until it is needed.

Some examples:
- The program wants the value for an arithmetic operation
- Pattern matching is to be performed
- The program wants to output a value


## Laziness and Infinite Data Structures

Laziness allows a program to work with data structures that are *conceptually infinite*.

```haskell
-- Infinite list starting at 1
[1..]
```
If you attempt to print this list, the program will run infinitely

An infinite list is typically referred to as a stream.



>[!example]
>**The Sieve of Eratosthenese**
>
>```haskell
>all_primes :: [Integer]
>all_primes = prime_filter [2..]
>
>prime_filter :: [Integer] -> [Integer]
>prime_filter [] = []
>prime_filter (x:xs) = 
>	x:prime_filter (filter (not . (`divisibleBy` x)) xs)
>```
So we're checking divisibility as we iterate up the list of natural numbers starting at the smallest prime, 2.

Notice that we're filtering and performing recursion on an infinite list (`xs`)


We can use `take` to *take* the first $n$ primes, or we could use `takeWhile` to take primes while a given condition is true


Laziness allows the programmer of `all_primes` to concentrate on the function's task - without having to pay attention to *how* the program wants to decide how many primes are enough
- Haskell will simply only compute as many as necessary


## Representing Unevaluated Expressions
The code needs to *remember* how to compute a value

Practically (under the hood), this is done by passing a function pointer to the calling expression.


**Parametric polymorphism** requires that the values of all types be representable in the same amount of memory.
- Without this, a function like `length` wouldn't be able to handle lists with elements of all types
- For any types that are larger than a single machine word, they will be allocated on the heap and a pointer will be passed instead.
- This standardises 'memory signature' of data types

Using this fact, the arguments of functions that are suspended can be stored in an *array of words* and a pointer to the function (so it doesn't matter what the types or function signature are).


### Evaluating lazy values only once
Many functions use the values of some variables *more than once*

To prevent unnecessary computation, once a value is computed it is recorded, and all subsequent uses of the value refer to that record.


## Call by Need
Operations such as:
- Printing
- Arithmetic operations
- Pattern matching
Start by ensuring their argument is *at least* partially evaluated

The ensure that at least the top level data constructor of the value is determined
- The arguments can remain suspensions


### Manipulating Control Flow

In the following Haskell function, the branch that isn't followed won't evaluate its respective function. This is *impossible* in an imperative language like C
```haskell
my_if :: Bool -> a -> a -> a
my_if cond t e -> if cond then t else e
```

We can use laziness to define our own efficient control structures
- Since un-followed paths won't evaluate



### Using laziness to avoid unnecessary work

A seemingly incredibly naïve implementation of `minimum` is:
```haskell
minimum = head . sort
```

In Haskell, this implementation actually isn't particularly inefficient because evaluation of the sorted list can stop immediately after the materialisation of the first element
- This is because `sort` uses selection sort by default, so it will stop after picking the first element


**Multiple Passes**

```haskell
output_prog_chars = do
	let anno_chars = annotate_chars 1 1 chars
	let tokens = scan anno_chars
	let prog = parse tokens
	let prog_str = show prog
	putStrLn prog_str
```

This function reads over an entire file multiple times.

This can be incredibly inefficient for imperative programs.
- In Haskell, the program works backwards, starts by trying to print the string and works backwards, computing only what is necessary

So we don't need to completely construct each of the data structures
- This saves a *huge* amount of memory, since laziness is driven by printing here

### Lazy Input

Given a file name, `readFile` returns the contents of the file as a string, but it returns the string *lazily*; it read the next character from the file only when the rest of the program needs that character.




