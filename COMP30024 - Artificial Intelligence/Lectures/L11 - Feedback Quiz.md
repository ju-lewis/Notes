
# 1.  Search

**Breadth-first search**
Expand: S, A, E, B, C, G1
Goal state reached: G1


**Uniform Cost Search**
Expand: S (0), A(6), C(8), B(10), E(10), D(13), G2(15)
Goal state reached: G2

**Greedy Search**
Expand: S, A, C, G2
Goal state reached: G2

**Is the heuristic admissible?**
No, consider state D, which is only at a distance of 2 from a goal state (G2). The heuristic over-estimates the actual cost here, resulting in the value 3.


# 2. Minimax

Max: `        6        `
Min:  ` 2            6  `
Max: `2, 8,        6, 7`

**2b.**
No, as we need to reach a terminal state in that sub-tree to know if we should prune it (which we should, as the MAX node is guaranteed to pick *at least* 8 if the game goes down that subtree)

**2c.**
Yes, as we can stop searching the middle subtree as soon as we reach the terminal state with a utility of 8.


# 3.  Environment Characteristics

Observable?: Yes
Deterministic?: Yes
Episodic?: No
Static?: Yes
Discrete?: Yes
