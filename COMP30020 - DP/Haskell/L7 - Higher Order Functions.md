
First order values are data

Second order values are functions
- Arguments are first or second order values

In general $n_{th}$ order values are functions who take $n$ or lower order values as input and return ${n-1}_{th}$ order values


### Infix Operators

Haskell allows you to make any function an infix operator by surrounding the name with *backticks* 

>[!example]
>```haskell
>is_even :: Int -> Bool
>is_even x = x `mod` 2 == 0
>```


## Anonymous Functions

In some cases, you only need a function once (e.g. for a single `filter` call)
	In this case, it's annoying to have to define an entire function


In Haskell, we can define anonymous functions using *lambda expressions*

```haskell
filter (\x -> x `mod` 2 == 0) [1,2,3,4]
```

The notation is based on the lambda calculus


### Lambda Calculus Fundamentals

Each argument is preceded by a lambda 
Argument list is followed by a dot and function body

>[!example]
>A function that adds together its 2 arguments:
>$\lambda a.\lambda b.a + b$

## Partial Application

Given a function with $n$ arguments, *partially applying* that function means giving its first $k$ arguments (where $k < n$)

The result of the partial application is a *closure* that records the identity of the function and the values of those $k$ arguments

The closure behaves as a function with $n-k$ arguments. A call of the closure leads to a call of the original function with both sets of arguments


>[!example]
>```haskell
>is_longer :: Int -> String -> Bool
>is_longer limit x = length x > limit
>```
>
>Now partially applying the function:
>```haskell
>filter(is_longer 4) ["ab", "abcd", "abcdef"]
>```
>
>The 'leftover' function from partially applying `is_longer` takes a string and returns whether it's longer than 4 characters



We can also partially infix operators by enclosing them in parentheses:
```haskell
Prelude> map (*3) [1,2,3]
[3,6,9]
```

### Types for Partial Application
In most languages, the type of a function with $n$ arguments would be:
`f :: (at1, at2, at3, ..., atn) -> rt`

In Haskell we absolutely can do this using `n-tuples`, but we can be smarter and design our function to use partial application

`f :: at1 -> at2 -> at3 -> ... -> rt`

So we take a value of type `at1` and we return a function that takes a value of type `at2` and so on, until we return a first order value of type `rt`


**Currying**

You can keep transforming the function type until every single argument is supplied separately. In Haskell, *all function types are curried.*

```haskell
is_longer :: Int -> String -> Bool
is_longer :: Int -> (String -> Bool)
```

We can see that `is_longer` takes an `Int` and returns a function that takes a `String` and returns a `Bool`


## Function Composition

We can compose more complex functions from basic ones, for example to find the minimum value within a list we can: 
1. Sort the list
2. Take the head of the list

Hence we can define a minimum function as:
```haskell
minimum = head . sort
```

This style of programming is called *point-free style*
	It would be better described as *value-free* however, since its distinguishing characteristic is the absence of variables representing first-order values

Read function compositions *right-to-left* (dot operator associates to the right)


Function composition is one way to express a sequence of operations
`step3f . step2f . step1f`

This idea is the basis of *monads*.


