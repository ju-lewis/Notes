
## Defining Search Strategies
- *Completeness* - does it always find a solution (if one exists)?
- *Time Complexity* - Number of nodes generated/expanded
- *Space Complexity* - Maximum number of nodes in memory
- *Optimality* - Does it always find a least-cost solution?

Time and space complexity are measured in terms of:
- $b$ - maximum branching factor of the search tree
	- How many actions can we apply at 
- $d$ - depth of the least-cost solution
- $m$ - maximum depth of the state space (may be $\infty$)


Uninformed strategies use only the information available in the problem definition
- Informed strategies use an additional heuristic

# Breadth-First Search
Expand shallowest unexpanded node.

Implementation:
	`QueuingFn` = put successors at the end of queue

Properties:
- Complete: yes
- Time: $O(b^d)$
- Space: $O(b^d)$
- Optimal: yes (if cost = 1 per step) as it always finds the shallowest solution

# Uniform-Cost Search
Expand least-cost unexpanded node

Implementation:
	`QueueingFn` = insert in order of increasing path cost

Properties:
- Complete: Yes, if step cost $\geq \epsilon$ 
- Time: Proportional to num. nodes with path cost $\leq$ optimal solution 
- Space: ^
- Optimal: Yes

# Depth-First Search
Expand deepest unexpanded node

Implementation:
	`QueueingFn`  = Insert successors at front of queue

DFS can end up in infinite cyclic behaviour if the problem domain is not a DAG.
- We can modify this to a graph search algorithm using state-checking

Properties:
- Complete: Only if depth is finite
- Time: $O(b^m)$ worst case is where we have to search to depth $m$ for every node
- Space: $O(bm)$ 
- Optimal: No

# Depth-Limited Search
Depth-first search with depth limit $l$

Implementation:
	Nodes at depth $l$ have no successors

# Iterative Deepening Search

Depth limited search with a constantly increasing search depth limit

Start with depth limit of 0, search for solutions
	If none found, increase depth limit

Repeat the iterative deepening until solution found, or max depth hit.

Properties:
- Complete: Yes
- Time: $O(b^d)$
- Space: $O(bd)$
- Optimal: Yest, if step cost = 1
	- Can be modified to explore uniform-cost tree


# Bidirectional Search
Search simultaneous from the start point, and backwards from the goal, and stop when the two searches meet in the middle

Problems:
- Generate predecessors; many goal states; efficient check for node already visited by other half of the search; and, what kind of search


Properties:
- Complete: Yes
- Time: $O(b^\frac{d}{2})$
- Space: $O(b^\frac{d}{2})$
- Optimal: Yes (If done with correct strategy - e.g. breadth first)




# Summary
- Formulate a single-state search problem
- Apply a search strategy to solve problem
- Analyse complexity of a search strategy
