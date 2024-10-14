

## Impacts of Laziness
Laziness adds some overhead
- Execution of a program creates a lot of suspensions
- Every access to a value must first check whether the value has been materialised yet

However, this can be balanced by also avoiding expensive computation

The dominant effect depends on the program and the kind of input it typically gets

>[!note]
>Usually the execution is a *little bit* slower, but sometimes it's *a lot* faster



### Strictness

The value of an expression whose evaluation loops infinitely or throws an exception is called "bottom", denoted $\bot$

A function is *strict* if it always needs the values of all its arguments.
In formal terms, this mean that if any of its arguments is $\bot$, then its result is also $\bot$

>[!example]
>The addition function `+` is strict.


GHC performs a strictness analysis - if a function is non-strict, then no suspensions will be generated.


### Unpredictability

Laziness can also make it harder for the programmer to understand where the program is spending most of its execution time


Remember, laziness is *demand-driven execution*


## Memory Efficiency

The necessity for copying in Haskell can result in memory inefficiencies, however compilers have many memory use optimisation
### Reusing Memory

Recall our binary search tree implementation in Haskell creates a new tree for any update (no destructive updates are possible)


The GHC compiler automatically reuses memory (when possible), for example nodes in the BST that are identical between trees are in *both at the same time*
- This is fine because there won't be any mutating operations on the nodes

On average, this means that we're only changing around $log_2(n)$ nodes

### Deforestations

If we're performing multiple traversals to iteratively create new (transformed) data structures

>[!example]
>`ds1 -> ds2 -> ds3`

If the programmer can restructure the code to avoid creating the intermediate data structures, the execution will be faster

>[!example]
>```haskell
>map (+1) $ map (2*) list
>```
>is equivalent to
>```haskell
>map ((+1) . (2*)) list
>```
>
>The second implementation is more efficient, succinct, and elegant

We can combine pairs of higher order functions to created deforested implementations of operations

We can also achieve deforested implementations with well-designed types


### Cords

Repeated appends to the end of a list are inefficient (quadratic in list length)

In declarative languages, we can use a data structure that supports constant-time appends

This is a possible implementation
```haskell
data Cord a = Nil | Leaf a | Branch (Cord a ) (Cord a)

append_cords :: Cord a -> Cord a -> Cord a
append_cords a b = Branch a b
```


The obvious algorithm to convert a `Cord` to a list is simply recursively appending (if not `Nil`), however this is also very inefficient


We can use an accumulator-based design to fix this
- The base case should just return the accumulated list so far
This prevents unnecessary recursion


## Removing Validity Checks

See how we can remove the empty list condition check from the recursive call to optimise the sorted check function:
```haskell
is_sorted :: Ord a => [a] -> Bool
is_sorted [] = True
is_sorted (x:xs) = sorted_lag x xs

sorted_lag :: Ord a => a -> [a] -> Bool
sorted_lag _ [] = True
sorted_lag x1 (x2:xs) = x1 <= x2 && sorted_lag x2 xs
```




