
# CSP Heuristics


## Minimum Remaining Values (MRV)

>[!Warning] Problem
> Which variable should be assigned next?

**Solution**:
- Choose the value with the fewest remaining legal values (*fail-first search*)

Most-constrained search

## Degree Heuristic

>[!Warning] Problem
>What is there is a tie-breaker among MRV variables?

**Solution**:
- Choose the variable with the most constraints on the remaining variables


## Least Constraining Value

>[!Warning] Problem
>In what order should values be tried?

**Solution**:
- For a given variable, choose the *least constraining value*
- The one that rules out the fewest values in the remaining variables


## Forward Checking

- Keep track of remaining legal values for unassigned variables
- Terminate search when any variable has no legal values

**Note**:
- Forward checking provides no early failure detection

# Constraint Propagation

## Arc Consistency
Simplest form of propagation makes each arc *consistent*

X -> Y is arc consistent iff:
- For every value x of X there is *at least one* value y of Y that satisfies the constraint (arc) between X and Y

### Arc Consistency Algorithm (AC3)


```
function AC3(csp) returns the CSP, possibly with reduced domains
	
	local variables queue (a queue of arcs, initially all arcs in csp)
	while queue is not empty do
		(Xi,Xj) = RemoveFirst(queue)
		if RemoveInconsistentValues(Xi, Xj) then
			foreach Xk in Neighbours(Xi) do
				add (Xk,Xi) to the queue
end

function RemoveInconsistentValues(Xi, Xj) true iff succeeds
	removed <- false
	foreach x in Domain(Xi) do
		if no y in Domain(Xj) allows (x,y) to satisfy Xi<->Xj then
			delete x from Domain(Xi)
		removed <- true
	return removed
end
```


Time complexity: $O(n^2d^3)$ (can be reduced to $O(n^2d^2)$ but detecting *all* is NP-hard)


## Subproblem Identification

If each subproblem has $c$ variables out of $n$ total, worst case solution becomes $O(\frac{n}{c} d^c)$, which is *linear* in $n$ 


## Tree-Structured CSPs

>[!Note] Theorem
>If the constraint graph has no loops, the CSP can be solved in $O(nd^2)$ time.

### Algorithm for tree-structured CSPs

1. Choose a variable as *root*, order variables from *root* to *leaves* such that every node's parent precedes it in the ordering 
2. For $j$ from $n$ down to $2$, apply `MakeArcConsistent(Parent(Xi), Xj)`
3. For $j$ from $1$ to $n$, assign `Xj` consistently with `Parent(Xj)`


>[!Example]
>First, order the variables from the root variable (topological sort)
>Then start at a leaf variable and trace back along the arcs, remove possible values from each variable to ensure consistency
>![[tree-csp-arc-consistency.png]]
> 


## Nearly-Tree Structured CSPs

**Conditioning**: Instantiate a variable, prune its neighbours' domains

**Cutset conditioning**: Instantiate (in all ways) a set of variables such that the remaining constraint graph is a tree

**Cutset**: a set of variables that can be deleted so that the constraint graph is a tree



# Iterative Algorithms for CSPs - Local Search


Hill-climbing search typically works with "complete" states, i.e. all variables assigned.
- Local search then tries to change on variable assignment at a time

>[!Example] Example: 4-Queens
>
>**States**: 4 queens in 4 columns (256 states)
>**Operators**: Move queen in column
>**Goal test**: no attacks
>**Evaluation**: $h(n)$ = number of attacks



