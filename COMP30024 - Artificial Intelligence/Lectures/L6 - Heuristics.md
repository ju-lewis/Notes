
# Admissible Heuristics

Recall that admissible heuristics are heuristic functions that never *overestimates* the actual 'distance' from the solution.

>[!example] 8-Puzzle Example
>**Heuristic 1**: $h_1(n)$ = number of misplaced tiles
>**Heuristic 2**: $h_2(n)$ = manhattan distance
>- Number of squares from the desired location of each tile


## Dominance
If $h_2(n) \geq h_1(n)$ for all $n$ (both admissible) then $h_2$ *dominates* $h_1$ and is better for search
- This is essentially just because it's a closer estimate of the actual goal cost


## Relaxed Problems
Admissible heuristics can be derived from the *exact* solution cost of a *relaxed* version of the problem.

>[!example] 8-Puzzle Example
>If the rules of the 8-puzzle are relaxed so that a tile can move *anywhere*, then $h_1(n)$ gives the shortest solution
>
>If the rules are relaxed so that a tile can move to *any adjacent square*, then $h_2(n)$ gives the shortest solution

# Iterative Improvement Algorithms

In many optimization problems, *path* is irrelevant; the goal state itself is the solution

Then state space = set of "complete" configurations;
	find *optimal* configuration (e.g. travelling salesman problem)
	find configuration satisfying constraints (e.g. n-queens)

In such cases, we can use *iterative improvement* algorithms;
keep a single "current" state, try to improve it.


Constant space, suitable for *online* and *offline* search.


>[!example] Travelling Salesperson Problem
>Find the shortest path that visits each city exactly once.
>
>Relaxed problem: let path be *any* structure that connects all cities
>- Use minimum spanning tree as a heuristic for TSP; complexity is $O(E\log E)$
>  
>  **Iterative Improvement**
>  We can perform a 'clockwise traversal' of the minimum spanning tree to obtain a minimum tour of the cities. We're iteratively improving the initial solution by swapping links.
>  


## Gradient Descent (Or Ascent)

"Like climbing Everest in thick fog with amnesia"

```
function HillClimbing(problem) returns a solution state
	inputs: problem: a problem
	
	current <- MakeNode(InitialState(problem))
	loop do
		next <- highest valued successor of current
		if Value[next] < Value[current] then return current
		current <- next
	end
```

**Problem**: Depending on initial state, can get stuck on local optima


# Summary
Heuristics help reduce search cost, however finding optimal solutions is still difficult.

Skills needed:
- Demonstrate operation of search algorithms
- Discuss and evaluate the properties of search algorithms
- Derive and compare heuristics for a problem
