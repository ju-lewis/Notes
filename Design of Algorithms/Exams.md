# Mid Semester Test
## 11am 28th March, Wilson Hall
## Content: **Lecture 1 - Lecture 6**
### Lecture 1
What is a problem?
What is an algorithm?
### Lecture 2
#### Primitive data structures:
- Array
- Linked List
#### Recursive Processing:
- Binary search (bounds are reduced by 1 on each update step: lo = mid + 1 OR hi = mid - 1)
#### Fundamental Data Structures:
- Stack (LIFO)
	- **Operations**
	- CreateStack
	- Push
	- Pop
	- Top (Peek)
	- EmptyStack
- Queue (FIFO)
### Lecture 3
#### Establishing Growth Rate:
- Big O (any function in this set grows faster ) WORST CASE
- Big Theta (any function in this set grows at the same rate)
- Big Omega (any function in this set grows faster) BEST CASE

Use L'Hopital's rule for computing the ratio of growth rate

#### Computing Number of Fundamental Operations with Sums
Beware the fenceposting error when calculating sums! (REMEMBER TO INCLUDE THE BOUND)

When computing cost recursively:
- Compute a base case ( i.e. M(0) )
- Compute the recursive case in terms of itself (i.e. M(n) = M(n-1) + 1 )

Remember that all logarithms can be written as a constant multiple of any other base, so all logs have the same asymptotic growth rate.
### Lecture 4

### Lecture 5
### Lecture 6


# Final Exam

## Topics I know I need to revise:
### Recurrence Relations
1. Computing closed form computational complexity for any given recursive problem
### Graph traversal (Prim's, Dijkstra's)
1. Pseudocodes
2. Different types of DFS and BFS for DAG/Tree structures
	1. DFS: Pre-order, In-order, post-order (works with recursion because of implicit stack)
	2. BFS: Level order
3. Topological sorting

###  Dynamic programming
1. Knapsack
2. Travelling salesman
3. *Interpreting general problems*
	1. Think about the sub-problems being solved, e.g. for a decision problem - should we choose the $n_{th}$ item?
		1. **REMEMBER THAT THE RECURSIVE CASES ARE BUILT UP FROM THE BASE CASES, NOT THE OTHER WAY AROUND**
	2. Find the base case(s)
	3. Find the recursive case
4. Warshall / Floyd
	1. Remember infinity for unknown
### String Search
1. Revise Horspool
### Sorting
1. Lomuto partitioning, Hoare partitioning
2. Different heap-sort approaches


## Examinable Content:
- Algorithm Design (Pseudocode)
- Data Structures
	- Advantages, disadvantages (time complexities)
- Asymptotic Notation
	- $O, \Omega, \Theta$
- Recurrence Equations
	- Telescoping
	- Master Theorem
- Divide-and-Conquer
- Graph Concepts and Graph Algorithms (Prim, Dijkstra)
	- Adjacency Matrix (Good for dense graphs $|E|\in O(|V|^2)$)
	- Adjacency List (Good for sparse graphs $|E|\in O(|V|)$)
- DFS, BFS, Tree Traversals, Topological Sorting
- String Search
	- Naive, Horspool
- Dynamic Programming
- Sorting
	- Comparison:
	- Distribution:
- Binary Search Trees:
	- Self-balancing trees
	- 2-3 Trees
- Hashing and Hash Tables
	- Separate Chaining
	- Linear probing (open addressing)
- Compression
	- Fixed length encoding
	- Run length encoding
	- Huffman compression (variable length encoding)
