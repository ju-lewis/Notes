
# 1. Toy Graphs

**1a.** A tree of depth 1 will have $\Theta(n)$ nodes generated when the root node is discovered
**1b.** A linked list (degenerate tree) will at most have 1 node in the generated state
**1c**. Any balanced tree would have this property

# 2. Iterative Deepening Search
**2a.** Derive the time complexity of IDS on a graph with branching factor $b$ and minimum goal depth $d$

We're effectively doing successive depth-first search on increasingly deep trees

**Operations:**
Depth 1: $b$
Depth 2: $b + b^2$
Depth 3: $b + b^2 + b^3$
...
Depth $d$: $b +b^2 + b^3 + ... + b^d$

So for a full search of a tree with min goal depth $d$ we get:
$$(b) + (b+b^2) + (b+b^2+b^3) + ... + (b+b^2+b^3+...+b^d) = O(b^d)$$ 
Hence the overall complexity is $O(b^d)$


**2b.** When the goal state is located at the maximum depth of the problem domain

**2c.** All paths must be weighted equally, i.e. when the shallowest solution is optimal.


# 3. Connected Components

1. Initialise the component counter to 0
2. Start DFS on a random *unvisited* vertex in the graph and increment the counter by 1, once DFS can no longer discover any vertices we know a connected component has been fully discovered.
3. Repeat *step 2* until there are no more unvisited vertices

# 4. Directed Graphs

**4a**.
We first need to represent the problem as a *directed graph* where vertices are the children and an edge from $V_a$ to $V_b$ represents child $a$ hating child $b$.

We can achieve this ordering using a form of topological sort with depth-first search.

1. Start at a vertex (child) with no incoming connections. This graph source vertex represents a child who is not hated by anyone.
2. Use DFS to traverse along their directed connections, adding the children to the *back* of the line as we visit the vertices. When there are no longer any undiscovered nodes we have completely visited a connected component within the directed graph.
	- This implies that no one in this component hates anyone from outside of the component
3. We can now pick another unvisited source vertex to begin traversing from again.
	- Because this is a separate connected component, we can safely place this entire new component at the front of the line (as they are unhated by people in other components)
4. Repeat until all children have been added to the line 

**4b.**

# 5. Diameters

$$\text{Tree Diamater } \Delta = \max_{v_1,v_2\in V}\delta(v_1,v_2)$$
In essence, the *diameter* of $T=(V,E)$ is the maximum number of edges between two vertices $v_1$ and $v_2$.

As 'lateral' distance between vertices can only change (either increasing or decreasing) when traversing *down* the layers of a tree, the maximum distance between 2 nodes will occur at the outer-most and deepest vertices of the tree.

We can discover these most-distant vertices by performing a DFS traversal of the tree:
- For every traversal we take, we note the 'lateral position' of the current vertex;  decreasing when traversing left and increasing when traversing right
- As we perform a full search through the tree we keep track of the left-most and right-most vertices discovered

At the end we're left with the most distant vertices on the tree, and hence have the diameter.

# 6. Keys and Rooms

```python

def can_visit_rooms(keys: set[int], 
	keys_in_rooms: list[set[int]], num_rooms: int) -> bool:
	
	n_visited = 0
	
	while keys != {}:
		# Pick a key from our currently held keys
		k = keys.pop()
		
		# Visit that room
		n_visited += 1
		keys.update(keys_in_rooms[k])
	
	# Determine if we have visited every room when we run out of keys
	if n_visited != num_rooms:
		return False
	
	return True

# Start off with the key to room 0 (since it's assumed to be unlocked)
print(can_visit_rooms({0}, []))

```




