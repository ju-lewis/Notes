

## Byrd Box Model

The Prolog debugger operates on the Byrd Box Model:
1. Execution of a predicate will initially enter through the `Call` *port*
2. Execution failure causes a return through the `Fail` *port*
3. Execution completion (success) returns through `Exit` *port*
4. If a goal after a nested choice point fails, it re-enters through `Redo` *port*


- Unify with a **fact**: immediately exit through `Exit` port
- Unify with the *head* of a *rule*: Issue a nested `Call` into another Byrd box, calling the goal with new bindings

If you can exit the nested boxes from the body of the rule, then exit through the `Exit` port


### Useful Debugger Commands:
- `r` (retry) restarts a goal from the beginning.
- `s` (skip) skips forward in time until an exit or fail port is reached from the current goal

**A quick way of tracking down bugs**:
1. When you arrive at a call or redo port: `skip`
2. If you come to an exit port with the correct results (or a *correct* fail port): `creep`
3. If you come to an *incorrect* exit or fail port: `retry`, then `creep`


Consider the following predicate relating a list to its reverse:
```prolog
rev1([], []).

rev1([A|BC], CBA) :- 
	append(CB, [A], CBA) ,
	rev1(BC, CB).
```

This predicate fails after finding the first solution when the first term is ground and the second term is non-ground. (`rev1(+ABC, -CBA)`)

This happens because the `append` predicate is called in the mode `append(-A, +B, -C)`, in essence, it's being asked to find a list `A`, when appended to a ground list `B`, yields a non-ground list `C` - to which there are obviously infinite solutions, e.g.:
1. `append([], [a], [a])`
2. `append([_], [a], [_, a])`
3. `append([_, _]), [a], [_, _, a]`
and so on.

All of these bindings will result in recursion down the `rev1` predicate call, until it is determined that the 2 lists cannot be unified as they are different lengths, so infinite repetition occurs.


**A solution**:
We can fix this by ensuring the compared lists are of the same length, thus preventing investigating choicepoints where this is not true.

```prolog
new_rev([], []).
new_rev([A|BC], CBA) :- 
	same_len([A|BC], CBA) ,
	rev1([A|BC], CBA).

same_len([], []).
same_len([_|Xs], [_|Ys]) :- same_len(Xs, Ys).
```

So now the lists will be bound to be the same length, preventing the program from hanging.

### Spypoints

If you have an idea of what predicates you suspect of being buggy - you can use spypoints (which function somewhat like breakpoints)

When Prolog reaches any port of a predicate with a spypoint, Prolog stops and shows the port.

1. `spy(pred).`  sets a spypoint on the named predicate
2. `nospy(pred).` removes spypoints from the predicate
3. `l` (leap) tells Prolog to run quietly until a spypoint is reached



## Documenting Prolog Code

Prolog files should have 2 levels of documentation:
1. File level docs
	1. Start with *purpose*, *author declaration*, *brief summary of code*
2. Predicate level docs
	1. Above all non-trivial predicates
	2. Identify: *what it does*, *usable modes*


Predicate level doc example:
```prolog
%% remove_duplicates(+List, -Result)
%
%  Removes the duplicates in List, giving Result
%  Elements are considered to match if they can be
%  unified with each other; thus, a partly 
%  uninstantiated element may become further 
%  instantiated during testing. If several elements
%  match, the last of them is preserved.
```


## Choicepoints and Efficiency

Consider the definition for a factorial predicate:
```prolog
fact(0, 1).
fact(N, F) :-
	N1 is N - 1 ,
	fact(N1, F1) ,
	F is N * F1.
```

This predicate will correctly compute the factorial of `N`, however a choicepoint is left open afterwards when the Prolog binds to the rule `fact(0, 1)`. This means that if we ask for more solutions, Prolog will continue recursively calling the `fact(N, F)` rule, decrementing each time into the negatives. This will never terminate, so we need to implement a guard to prevent infinite recursion.

We can fully describe factorial (including specifying the necessity of positive values) like so:
```prolog
fact(0, 1).
fact(N, F) :-
	N > 0 ,
	N1 is N - 1 ,
	fact(N1, F1) ,
	F is N * F1.
```

However, as Prolog recurses down to the `fact(0, 1).` base case, a choice point is left open as this could also unify with `fact(N, F)` through the substitution N=0, F=1

Luckily this fails quickly, however it still significantly reduces the ability to optimise the predicate using *last call optimisation*.


### If-Then-Else Construct

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

Here, the arrow (`->`) tells Prolog that if the condition on the left (e.g. `N =:= 0`) is met, then everything after the `;` can be ignored, and vice versa if the condition fails. This removes the possibility of choicepoints for mutually exclusive outcomes.

**HOWEVER**, you should avoid using if-then-else if indexing (creating separate rules/facts) can be done, as if-then-else is far less multimodal.


