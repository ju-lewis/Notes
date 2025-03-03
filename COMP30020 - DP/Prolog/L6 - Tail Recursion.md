
 A predicate is *tail recursive* if the only recursive call is the last code executed before returning to the caller.

The definition of `append/3` is tail recursive
```prolog
append([], C, C).
append([A|B], C, [A|BC]) :-
		append(B, C, BC).
```
If there was anything after the recursive call to `append`, then it would *not* be tail recursive

Prolog performs *tail recursion optimisation* (TRO), which makes recursive predicates behave as if they were loops


## The stack
When a predicate `a` is called, a *stack frame* is created in the stack data structure. When `a` calls `b`, another *stack frame* is added.

The stack very quickly grows - TRO helps optimise this.

If all `b` does after calling `c` is return to `a`, we can prematurely remove `b`'s stack frame to save space and time.


### TRO and Choicepoints

TRO is a special case of *last call optimisation* where the last call is recursive

If `b` leaves a choicepoint, it sits on the stack above `b`'s frame "freezing" that and all preceding frames, so they can't be reclaimed. This is done so Prolog can return to `b` when backtracking.
![[TRO.png]]

So, for TRO to work - the predicate must be deterministic.


## Optimisation

#### Making a predicate tail-recursive
Sometimes you can make code tail recursive by simply re-ordering the body of the rule.


Despite having multiple distinct cases (i.e. base case, recursive case) - this definition of factorial avoids any choicepoints by using the `if-then-else` construct
```prolog
fact(N, F) :-
	( N =:= 0 -> 
		F = 1
	;   N > 0,
		N1 is N - 1 ,
		fact(N1, F1) ,
		F is F1 * N
	).
```

However, we currently cannot make it subject to TRO, as the `is/2` predicate requires the right argument to be ground - meaning we cannot put the `fact/2` call as the last line

#### Adding an accumulator
An accumulator is an extra parameter that holds a partially computed result

The key to getting the implementation correct is specifying what the accumulator *means* and how it relates to the final result.


This accumulator method accumulates the result as it gets recursively called, finally binding `F` to the result at the base case - instead of updating `F` for every recursive call.
```prolog
fact1(N, A, F) :-
	(N =:= 0 ->
		F = A
	;
		N > 0,
		N1 is N - 1,
		A1 is A * N,
		fact1(N1, F, A1)
	).
```
We 'hold on to' `F`, and finally bind it at the end.

It helps thinking 'imperatively' to determine how the accumulator is integrated


#### Transformation

Another approach is to transform the non-tail recursive version into an equivalent tail recursive predicate.

Start by defining a new predicate to do the work of the old one, and everything following it

##### Example:
Transforming `fact` predicate
```prolog
fact1(N, A, F) :-
	fact(N, F2),
	F is F2 * A.
```

Then *unfold* the call to the non-tail recursive predicate
```prolog
fact1(N, A, F) :- 
	( N =:= 0 -> 
		F2 = 1
	;   
		N > 0,
		N1 is N - 1 ,
		fact(N1, F1) ,
		F2 is F1 * N
	),
	F is F2 * A.
```

Next, we move the final goal into the *then* and *else* branches
```prolog
fact1(N, A, F) :- 
	( N =:= 0 -> 
		F2 = 1 ,
		
		F is F2 * A
		
	;   
		N > 0,
		N1 is N - 1 ,
		fact(N1, F1) ,
		F2 is F1 * N ,
		
		F is F2 * A
		
	)
```

The next step is simplifying the arithmetic,
1. All the '*then*' block did was unify `F2` with `1`, and `F` with `A*F2` - this can be simplified
2. In the '*else*' block, we can skip unifying `F2` as well by combining the arithmetic

```prolog
fact1(N, A, F) :- 
	( N =:= 0 -> 
		F is A
	;   
		N > 0,
		N1 is N - 1 ,
		fact(N1, F1) ,
		F is (F1 * N) * A
	)
```

Now part of the computation can be moved before the call to `fact/2`
```prolog
fact1(N, A, F) :- 
	( N =:= 0 -> 
		F is A
	;   
		N > 0,
		N1 is N - 1 ,
		A1 is N * A ,
		fact(N1, F1) ,
		F is F1 * A1
	)
```

The final step is recognising that the last 2 goals look like the body of the original definition for `fact1/3`

```prolog
fact1(N, A, F) :- 
	( N =:= 0 -> 
		F is A
	;   
		N > 0,
		N1 is N - 1 ,
		A1 is N * A ,
		fact1(N1, A1, F)
	)
```


### Accumulating Lists

Consider the following definition of a predicate to reverse a list:
```prolog
rev1([], []).
rev1([A|BC], CBA) :- 
	rev1(BC, CB),
	append(CB, [A], CBA).
```

This predicate is of *quadratic complexity* because for the $n^{th}$ element from the end of the first argument, we append a list of length $n-1$ (remember a call to `append/3` is linear-time)

We want to make `rev1/2` tail recursive. Our new predicate must combine the work of `rev1/2` with `append/3`


```prolog
% rev(BCD, A, DCBA)
% DBCA is BCD reversed, with A appended

rev([], A, A).
rev([B|CD], A, DCBA) :-
	rev(CD, [B|A], DCBA).
```

![[Transformation.png]]


The trick used for a tail recursive `rev/3` predicate is often used in Prolog:
	A predicate that generates a list takes an *extra argument* specifying what should come after the list (avoiding an append call)


If you don't know what'll come after at call time:
1. Pass an unbound variable
2. Bind that variable when you *do* know what should come after

Because of this technique, many predicates that produce a list have *2 additional arguments*:
- One denotes the list produced
- The other is what comes after
This is called a difference pair - as the predicated generates the difference between the 1st and 2nd of these lists

