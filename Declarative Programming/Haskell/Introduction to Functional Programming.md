

The basis of functional programming is *equational reasoning*.

>[!note]
>If 2 expressions have equal values, then one can be replaced with the other.


## Lists

Empty list: `[]`
Non-empty list: `x:xs`
	`:` is the list constructor.

The notation `[1,2]` is syntactic sugar for `1:2:[]`

## Functions

A function definition consists of equations, each of which establishes an equality between the left and right hand sides of the equal sign.

>[!example]
>```haskell
>len [] = 0
>len (x:xs) = 1 + len xs
>```

Function definitions use *pattern matching*

Patterns should be *exhaustive*. (At least 1 pattern applies to any call)
It is good practice to ensure the patterns are *exclusive* as well.

If patterns are *exclusive* and *exhaustive* then exactly 1 pattern will apply for any call.

## Syntax
### Function calling
```haskell
f a1 a2 a2
```
calls function `f` with arguments `a1`, `a2`, `a3`

We use parenthesis for *grouping* 

```haskell
f a1 (g a2) a3
```
calls `f` with `a1`, the result of calling `g` with `a2`, and `a3`


### Layout

**The offside rule**:
if 'line1' starts in column `n` and 'line2' starts in column `m`:
- `m > n`: line2 is a continuation of the construct on line1
- `m = n`: line2 is the start of a new construct (same level as line1)
- `m < n`: line2 is the continuation of something else that line1 is part of

>[!tldr]
>Indentation must match structure.
>
>Never use tabs.


## Recursion
Haskell has no looping construct - we must use recursion and higher order programming.

## Expression evaluation
Haskell:
1. Looks for a function call in the current expression
2. Searches the list of equations defining the function from the top down
3. Sets the values of the variables in the matching pattern to corresponding args
4. Replaces left hand side of the equation with the right hand side.

### Order of evaluation
The result will always be the same! The Church-Rosser theorem proved order of evaluation doesn't matter for the *lambda calculus*

**HOWEVER**
Order of evaluation *does* have an impact on efficiency.



## Declarative vs Imperative

**Side effects**
In the presence of side effects, a program's behaviour depends on history.
	Order of evaluation matters.

This makes a program harder to understand.

Declarative programs do not allow side effects.
(*other than exceptions*)

### Referential Transparency
Equational reasoning.

If we see an expression with a value - we can take it out and replace it with the value.

Haskell is a single assignment language.


## Variables

Using the explicit `let` syntax
```haskell
let pi = 3.14159
```







