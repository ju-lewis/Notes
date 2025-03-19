Applying heuristics to go from uninformed search strategies to *informed* search strategies

# Best-First Search

>[!note] General Idea
>Use an *evaluation function* for each node
>- Estimate of desirability
>- Expand the *most desirable* unexpanded node.

`QueueingFn` = insert successors in decreasing order of desirability

**Special cases:**
- Greedy Search
- A* Search

## Greedy Search
Evaluation function $h(n)$ (the heuristic) = estimate of cost from $n$ to $goal$

>[!example] Romania Holiday Example
>$h_{SLD}(n)$ = straight-line distance from $n$ to Bucharest

Greedy search expands the node that *appears* to be closest to the goal.
- Because of this, it's not guaranteed to find a globally optimal solution

### Properties:
**Complete**: No, can get stuck in loops (unless we have repeated state checking and the space is finite)
**Time**: $O(b^m)$, but a good heuristic can give dramatic improvement
**Space**: $O(b^m)$, keeps all nodes in memory
**Optimal**: No.

## A* Search
**Idea:** avoid expanding paths that are already expensive.

Evaluation function $f(n) = g(n) + h(n)$
- $g(n)$ = cost so far to reach $n$ (path cost)
- $h(n)$ = estimated cost to goal from $n$
- $f(n)$ = estimated total cost of path through $n$ to goal

A* search uses an *admissible* heuristic
- $h(n) \leq h^*(n)$ where $h^*(n)$ is the *true* cost from $n$
- In essence, $h(n)$ must never overestimate the true cost.

>[!example] Romania Holiday Example
>$h_{SLD}(n)$ never overestimates the actual road distance

**Theorem**: A* search is optimal

### Optimality of A*
**Lemma**: A* expands nodes in order of increasing $f$ value

Gradually add "$f$-contours" of nodes (cf. breadth-first add layers)
Counter $i$ has all nodes with $f = f_i$ where $f_i < f_{i+1}$

### Properties:
**Complete**: Yes, unless there are infinitely many nodes
**Time**: Exponential in \[relative error in $h \times$ length of soln. \]
**Space**: Keeps all nodes in memory
**Optimal**: Yes, cannot expand $f_{i+1}$ until $f_i$ is finished


