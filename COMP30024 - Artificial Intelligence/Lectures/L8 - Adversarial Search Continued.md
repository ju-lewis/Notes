

# Minimax Continued

Weighting a linear sum of features for our *evaluation function*
- The exact weight doesn't matter too much

Behaviour is preserved under any *monotonic* transformation of `Eval`
Only the order matters:
- Payoff in deterministic games acts as an *ordinal utility* function

Hence, there is a *set* of values that will work as weights for this evaluation function.

>[!example]
> These search trees lead to equivalent outcomes
> ![[minimax-weights.png]]

## Cutting off Search
`MinimaxCutoff` is identical to `MinimaxValue` except:
- `Terminal?` is replaced by `Cutoff?`
- `Utility` is replaced by `Eval`
	- Because we need to evaluate intermediate states without scoring based on the outcome of the game.

Does it work in practice?
$b^m = 10^6$
$b=35 \implies m=4$ 

4-ply lookahead isn't enough for games like chess.
- Around the level of a human novice

# $\alpha$-$\beta$ Pruning

We can prune certain branches of the search tree if they're not going to influence the outcome of the game.

**General Approach**
As we recursively search down paths we can stop searching branches if we know those states won't be reached (due to the behaviour of `max` nodes or `min` nodes) 

>[!example]
>If the left-most branch in a search tree has a *maximum* value of 3, and we begin searching a middle branch, which reveals an outcome with value 2 below a *minimum layer* (hence has a maximum value of 2), we can immediately stop searching that branch as we know it'll *at best* result in a value of 2 (against an optimal player).
>
>![[alpha-beta-pruning.png]]


## Properties of $\alpha-\beta$
Pruning does not affect the final result

Good move ordering improves the effectiveness of the pruning

With "perfect doubling", the time complexity becomes $O(b^{m/2})$
- Doubles every search
- Can easily reach depth 8 and play good chess


## The $\alpha-\beta$ algorithm

```
function MaxValue(state, game, a, b) returns the minimax value of state
	inputs: state current state in game
			game: game description
			a: the best score for MAX along the path to state
			b: the best score for MIN along the path to state
			
	if CutoffTest(state) then return Eval(state)
	for each s in Successors(state) do
		a <- Max(a, MinValue(s, game, a, b))
		if a >= b then return b
	end
	return a

function MinValue(state, game, a, b) returns the minimax value of state
	if CutoffTest(state) then return Eval(state)
	for each s in Successors(state) do
		b <- Min(b, MaxValue(s, game, a, b))
		if b <= a then return a
	end
	return b
```


# Nondeterministic Games

We now add an additional element to our search trees
- A chance node

So we now need to consider the outcome of the random choice
- At each chance node, we compute the *expected value* of the possible outcomes

## Expectiminimax
The algorithm is just like minimax, but we must also handle chance nodes

```
if state is a chance node then
	return average of ExpectiminimaxValue of Successors(state)
```


>[!note]
>As the depth increases, the probability of ending up in a specific game state becomes significantly less likely; if the world is very uncertain - what's the point in trying to predict the future?
>
>Value of lookahead is greatly diminished

$\alpha-\beta$ pruning is much less effective.


In our evaluation function, exact values *do* matter.
- Behaviour is preserved only by *positive linear transformations* of `Eval`

Hence `Eval` should be proportional to the expected payoff

# Summary
- Understand game search algorithms
- Evaluation function
- Search in nondeterminism games

