## Problem Solving Steps
- Understand the problem
- Decide of computational means 
- Decide on method to use
- Decide the necessary data structures and algorithms
- Check for correctness
- Evaluate analytically
- Code it
- Evaluate empirically

## Primitive Data Structures:
### Arrays
### Linked Lists

**Insertion Time:**
- Unsorted: $O(1)$
**Search Time:** 
- Unsorted:  $O(n)$

```c
typedef struct node node_t;

struct node {
	void *data;
	node_t *next;
};

typedef struct {
	node_t *head;
	node_t *tail;
} list_t;
```

## Recursive Problem Solving

## Abstract Data Types
***An ADT is like a set of promises, or intended features.***
### Stack (LIFO)
Operations:
- CreateStack
- Push
- Pop
- Top
- EmptyStack? (Prevents popping from empty stack)
### Queue (FIFO)
Operations:



## Algorithm Analysis
**Resources consumed: *time* and *space**.*

We want to assess efficiency as a function of input size:
- Mathematical vs empirical assessment
- Best/Average/Worst case performance

If *c* is the cost of a *basic operation* and g(n) is the number of times the operation is performed for input of size n,
<div style="text-align: center;">running time t(n) ≈ c*g(n)</div>



### Basic Operation Examples:

| Problem                         | Size Measure          | Basic Operation      |
| ------------------------------- | --------------------- | -------------------- |
| Search in list of n items       | n                     | Key comparison       |
| Multiply two matrices of floats | Matrix size           | Float multiplication |
| Graph Problem                   | Number of nodes/edges | Visiting a node      |

**Analysis Types:**
- Worst-case
- Best-case
- Average-case (assuming that your input is randomly drawn from all possible inputs of size *n*)
- Amortised analysis takes the context of a running algorithm into account and calculates cost *spread over many runs*


### Asymptotic Analysis
We are interested in *growth rate* of functions:
- ignore constant factors
- Ignore small input sizes

$$ f(n) \prec g(n) \iff \lim_{n\to\infty}\frac{f(n)}{g(n)}=0$$


### Big-Oh Notation

We write $t(n)\in O(g(n))$ when, for some $c$ and $n_0$,

$$n > n_0 \implies t(n) < c \cdot g(n)$$
*For any constant $n$, there is a multiple of $g(n)$ that is greater than $t(n)$*

For example,
$$ 1 + 2 + ... + n = \frac{(n+1)n}{2} \in O(n^2) $$

#### What are the pitfalls of Big-Oh notation?
As $O$ provides an upper bound, it is correct to say:

 $3n \in O(n^2)$ AND $3n \in O(n)$

Since $O(n^2)$ simply states that any function within that set will grow at the same rate or slower than $n^2$ asymptotically (which $3n$ obviously satisfies) 

In the case of $O(n)$ and $3n$, the key is that they grow at the same rate *asymptotically* as the constant factor becomes insignificant.



### Big-Omega and Big-Theta

$\Omega(g(n))$ denotes the set of functions that grow **no slower than $g$**, so $\Omega$ is for *lower* bounds. (So the big-omega notation of a function means the algorithm will always take longer to execute than $g(n)$)


$\Theta(g(n))$ is for *exact* order growth.


### Runtime notation summary:

| Notation      | $O(f(n))$                                       | $\Omega(f(n))$                                  | $\Theta(f(n))$     |
| ------------- | ----------------------------------------------- | ----------------------------------------------- | ------------------ |
| Set           | Functions that grow slower (or the same as) $f$ | Functions that grow faster (or the same as) $f$ | Exact order growth |
| Runtime Bound | Upper (Worst)                                   | Lower (Best)                                    | Exact              |


### Establishing Growth Rate

For some $c$ and $n_0$, a common approach uses:

$\lim_{n\to\infty}{\frac{t(n)}{g(n)}} = 0 \implies t$ grows slower than $g$

$\lim_{n\to\infty}{\frac{t(n)}{g(n)}} = c \implies t$ and $g$ have the same order of growth

$\lim_{n\to\infty}{\frac{t(n)}{g(n)}} = \infty \implies t$ grows faster than $g$

L'Hopital's rule is incredibly useful for this

---
#### Example -  Show $1000n \in O(n^2)$

$$
\lim_{n\to\infty}{\frac{t(n)}{g(n)}} = \lim_{n\to\infty}{\frac{n^2}{1000n}}
$$
$$
= \lim_{n\to\infty}{\frac{1}{1000}n} = \infty
$$
Hence, $n^2$ grows faster than $1000n$, so $1000n \in O(n^2))$

---

#### Calculating Growth Rate of Selection Sort

```psuedocode
function SelSort(A[0..n-1])
	
	for i <- 0 to n-2 do
		min <- i
		
		for j <- i+1 to n-1 do
			if A[j] < A[min] then
				min <- j
		swap A[i] and A[min]
```

Basically,
1. Create index `i` into the array, starting at 0
2. Find the smallest value from `i` to the end of the array
3. Place the smallest value at `i`
4. Increment `i`

When `i` reaches the end of the array, it will be sorted

**Computing time complexity**
(Keep in mind, the below expressions describe the number of basic operations performed - where we define the basic operation to be the swap)
$$t(n) = \sum^{n-2}_{i=0}{\sum^{n-1}_{j=i+1}{1}}$$
$$t(n)=\sum^{n-2}_{i=0}{(n-1-i)} = (n-1)^2 - \sum^{n-2}_{i=0}{(i)}$$

The reason the inner sum = $(n-1-i)$ instead of $(n-2-i)$ is the inclusivity of sums. $(n-2-i)$ is a fence-post error.'

*Note that we can perform the above step as $n-1$ is a constant with respect to $i$*
$$t(n) = (n-2) + (n-3) + ... + ((n-2)-(n-2)) $$
$$t(n) = \frac{n(n-1)}{2} = \Theta(n^2)$$

### Analysing Recursive Algorithms (Telescoping)

**A simple example (recursive factorial calculator):**
```psuedocode
function F(n)
	if n=0 then return 1
	else return F(n-1)n
```

The basic operator here is the multiplication (so time complexity is in terms of number of multiplications).

We express the cost recursively as well:
$M(0) = 0$
$M(n) = M(n-1)+1 \: for \: n>0$

Since
$M(n-1) = (M(n-2) + 1) + 1 = M(n-2)+2$

We can keep going
$M(n) = M(n-1)+1 = M(n-2)+2 = M(n-3)+3 = M(n-n)+n = M(0) + n = n$
Using the base case, $M(0) = 0$ to finish.

#### Keep the *Smoothness Rule* in mind


*All logarithmic functions have the same asymptotic rate of growth:*
$$log_a{x} = (log_a{b})(log_b{x})$$
So we can rewrite any logarithmic function as a constant multiple of another.


### Some Useful Formulae:

From Stirling's formula: 
$$n! = O(n^{n+\frac{1}{2})})$$

Some useful sums:
$$\sum^{n}_{i=0}{i^2} = \frac{n}{3}(n+\frac{1}{2})(n+1)$$
$$\sum^{n}_{i=0}{(2i+1)} = (n+1)^2$$
$$\sum^{n}_{i=1}{\frac{1}{i}} = O(\log n)$$

# Week 3

## Brute Force Algorithms
Usually based directly on the problem's statement.

### Properties of Sorting Algorithms
A sorting algorithm is:
- **in-place** if it does not require additional memory (aside from variables)
- **stable** if it preserves the relative order of elements that have identical keys.
- **input-insensitive** if its running time is fairly independent of input properties other than size



*Selection Sort* is a brute force algorithm as we iterate over the entire set to find the absolute minimum until the array is sorted. It has an $\Theta(n^2)$ running time, but only makes about $n$ *exchanges*. So, it's good for small collections of large records.

### Brute Force (Naïve) *String Matching*:

Let P be the pattern (needle) to search for
Let T be the text (haystack) to search in

```psuedocode
Let n be length of T
Let m be length of P

for i <- 0 to m-n do
	
	j <- 0
	while j < m do
		if T[i+j] = P[j] then
			j <- j + 1
			
			if j = m then
				return i
		else
			break

```


### Brute Force Geometric Algorithms: Closest Pair

***Problem:*** Given *n* points in *k-dimensional* space, find a pair of points with minimal separating Euclidean distance.

If we were to consider *all possible* pairs as a brute force approach, we can already see that the running time will be undesirable:

1. Iterate through all points
2. Iterate though all other points for each point
3. Calculate distance at each pair, keep track of minimum

It is trivial to see that is algorithm is $\Theta(n^2)$

Note that we can speed up the algorithm *considerably* by utilising the monotonicity of the square root function. A clever divide-and-conquer solution yields a $\Theta(n log(n))$



## Exhaustive Search
#### Problem Type:
- Combinatorial decision or optimisation problems
- Search for an element with a given property
- Domain grows exponentially, for example all permutations

### Examples:
- Travelling Salesperson
- Knapsack
- Hamiltonian Tours
	- Given an undirected graph, is there a *simple tour*? (A path that visits each node once and returns to the start)
- Eulerian Tours
	- Given an undirected graph, is there a path which visits each *edge* exactly once?


For many optimisation problems, we do not know of solutions that are essentially better of exhaustive search.


## Graph Problems

One instance of the *exhaustive search* paradigm is *graph traversal*.

We'll begin by looking at 2 ways of visiting every node of a graph:
**Depth-first search** and **breadth-first search**

### Graphs, mathematically:

$G = \langle V, E \rangle$ 
V: Set of nodes
E: Set of edges (a binary relation on V)

![[Graph_1.png]]

![[Graph_concepts.png]]

### Some graph concepts:

#### Classification:
- Undirected / Directed
	- No indication of direction of traversal / Direction indicated
- Connected / Not connected
- Unweighted / Weighted
- Dense / Sparse
- Cyclic / Acyclic (actually, a *tree*)
- Directed cyclic, Directed acyclic (a *dag*)

#### Degrees of Nodes

If $(u, v) \in E$ then $u$ and $v$ are *adjacent*, or *neighbours*.

$(u,v)$ connects $u$ and $v$,      $u$ and $v$ are *incident* to $(u,v)$.

The *degree* of node $v$ is the umber of edges incident to v

For directed graphs, we talk about v's *in-degree* (number of edges going *to* v) and its *out-degree* (number of edges going *from* v)

#### Paths
A *path* in $\langle V, E \rangle$ is a sequence of nodes $v_0, v_1, ..., v_k$ from $V$, so that $(v_i, v_i+1)\in E$

A *simple path* is one that has no repeated nodes.
A *cycle* is a simple path, except that $v_0 = v_k$, that is, the last node is the same as the first node.

#### Rooted Trees
A (free) tree is a connected acyclic graph.

A rooted tree is a tree with one node identified as special. Every other node is reachable from the root node.

When the root is removed, a set of rooted sub-trees remain.

#### Graph Representations
- Adjacency Matrix
	- $k\times k$  matrix containing the number of direct paths between each node
	- Good for dense graphs
- Adjacency List
	- A vertical list of all nodes with "->" delimited lists containing all of the immediately reachable nodes.
	- Good for sparse graphs

# Week 4
### Depth-First Search

DFS corresponds to using a *stack discipline* for keeping track of where we are in the overall process

Levitin uses a more compact notation for the stack's history:

$$
a_{x,y}
$$
The first subscript (`x`) represents the order at which the node (`a`) is *pushed* onto the stack
The second subscript (`y`) represents the order at which the node is *popped* off the stack.

#### The Depth-First Search Forest
DFS trees

#### The Algorithm

#### Applications of DFS


### Breadth-First Search

BFS uses a *queue discipline* for keeping track of pending tasks

Example of how the queue develops (In essence, when a node is reached and dequeued, queue any of its immediate children):

```
(b) <- (a) -> (c) -> (d)
```

Queue:
$a_1$ Start by visiting first node
$b_2 \ c_3$ Queue the immediate 'children'
$c_3$ Visit immediate 'children'
$d_4$ If any further nodes are found, queue them

#### The Breadth-First Search Forest
We rewrite the graph to more clearly show the breath-first approach to searching, where cross-edges (edges that don't impact the search as they connect 2 nodes of equals depths) are dashed lines

#### The Algorithm


BFS has the same complexity as DFS.

Again, the same algorithm works for directed graphs as well.

Certain problems are more easily solved by adapting BFS



### Topological Sorting
Assume a directed edge from `a` to `b` means that `a` task must be completed before `b` can be started.

Then the graph has to be a DAG.

Assume the tasks are carried out by a single person, unable to multi-task

Then we should try to *linearise* the graph.

We first choose the *source* node (one that has no incoming edges)

#### We can solve the topological sorting problem with DFS:
<p style="text-align: center; color: red; font-weight: bold;">Only works when the graph is a DAG</p>
1. Perform DFS and note the order in which nodes are popped off the stack
2. List the nodes in the *reverse* of that order

This works because of the stack discipline. if `(u,v)` is an edge then it is possible to arrive at a DFS stack with `u` sitting below `v`.

Taking the "reverse popping order" ensures that `u` is listed before `v`.


# Week 5

## Greedy Algorithms

A *Greedy* algorithm is *locally optimal*.

For example, suppose we want to pay for something exactly with 50, 20, 10, and 5 cent coins. A *greedy* strategy would entail using as many 50 cent coins as possible before going on to 20 cents.


In general, we cannot expect *locally best* algorithms to yield a *globally optimal* result.


### Priority Queues
Priority queues are an abstract data structure that allow for the accessing the element of the highest priority.

This is very useful for greedy algorithms.

#### PQ Operations:
`inject(e)` 
`eject(e)`


### Spanning Trees

Recall that a *tree* is a connected graph with no cycles

A *spanning tree* of a graph is a tree where all of the edges are a subset of the edges in the original graph.

#### Minimum Spanning Trees of Weighted Graphs
If we have weighted edges, we can find the 'cheapest' path between 2 nodes by finding the minimum spanning tree.

Given a weighted graph, a sub-graph which is a tree with *minimum* weight is a *minimum spanning tree* for the graph

### Prim's Algorithm *(Greedy)*
![[Prims.png]]


# Week 6

## Binary Trees


## Binary Tree Traversal
### Pre-order Traversal
1. Print current node
2. Recurse on child nodes

We can implement pre-order traversal explicitly using a stack
```
while stack not empty:
	curr <- pop(T)
	visit(curr)
	
	push(curr_right)
	push(curr_left)
```

### Level-order Traversal

We can implement level-order traversal explicitly using a queue
```
while queue not empty:
	curr <- dequeue(T)
	
	
```
### Post-order Traversal
1. Recurse on both child nodes
2. Print current node

Note: the starting node will always be printed last
### In-order Traversal
1. Recurse on left node
2. Print current node
3. Recurse on right node



## Closest Pair Problem - Revisited

The brute-force method had complexity $\Theta(n^2)$, we can achieve $\Theta(nlog(n))$ with a divide-and-conquer approach.

### Approach:
- First sort the points by x value and store the result in array `byX`
- Sort the points by y value and store the result in array `byY`
- Now we can identify the *x median* and recursively process the set $P_L$ of points with lower x values and the set $P_R$ with higher x values.
- We can the identify $d_L$ (Shortest distance in $P_L$), $d_R$ (Shortest distance in $P_R$)
- Let $m = x \ median$ and $d = min(d_L, d_R)$ (d may be the smallest distance at this stage)
	- There is an edge case where the closest pair lies on either side of $m$
	- For these, we only need to look at points in the domain $\{m-d \leq x \leq m+d\}$, so pick from array `byY` each point `p` with x-coordinate in the domain and keep these points in array `S`
	- For each point in `S` consider only its 'close' neighbours.


```
minsq <- d^2

copy all point of byY with |x-m| < d to array S

k <- length(S)
for i <- 0 to k-2 do
	j <- i + 1
	
	while j <= k - 1 and (S[j].y - S[i].y)^2 < minsq do
		minsq <- min(minsq, (S[j].x - S[i].x)^2 + (S[j].y - S[i].y)^2)
		j <- j + 1
```

It can be shown that the while loop can execute *at most 5 times for each i value*



## Master Theorem

What is the time required to solve a problem size n by divide-and-conquer

For the general case, assume we split the problem into *b* instances (of size *n/b*), of which *a* need to be solved:

$T(n) = aT(n/b) + f(n)$

For integer constants `a >= 1, b > 1`  and function $f$ with $f(n) \in \Theta(n^b)$ time complexity and $T(1) = c$

$$ T(n) = \ \  \Theta(n^d) \ if \ a < b^d$$
$$T(n) = \ \ \Theta(n^d log(n)) \ if \ a=b^d$$
$$T(n) = \ \ \Theta(n^{(log_b(a))}) \ if \ a > b^d$$
## String Searching
### Brute Force
- $O(mn)$ complexity


### BMH
- Pre-process pattern to log the leftmost occurrence of each character
- Searches pattern right to left
- If a character in the text is found that is NOT in the pattern, shift by the length of the pattern

#### Case 1:
- The last character isn't in the pattern. *Shift by pattern length*

#### Case 2:
- The last character does not match but it's in the pattern. *Shift the pattern until the last occurrence of the character*
#### Case 3:
- The last character matches but one of the $m-1$ characters does not match and the last character is unique. *Shift by pattern length*
#### Case 4:
- The last character matches but one of the $m-1$ character does not match and the last character is not unique. *Shift pattern until the 2nd last occurrence of the character*

### Better Explanation:
- If there is a mismatch and the text has the last character, shift by pattern length
- Otherwise if there is a mismatch shift by the distance from the leftmost occurrence of the text's character to the end of the pattern

Example:
```
EAGLE
S = [3,5,5,5,4,5,2,5,5,5,5,1,5,5,5,5,5,5,5,5,5,5,5,5,5,5]
(E: 4, A: 3, G: 2, L: 1)
```

#### Pre-processing 

a is the size of the alphabet
```
function FindShifts(P[0..m-1])
	for i <- 0 to a - 1 do
		Shift[i] <- m
	
	for j <- 0 to m - 2 do
		Shift[P[j]] <- m - (j+1)
	return Shift
```

First initialise Shift array with the length of the pattern



```
function Horspool(P[0..m-1], T[0..n-1])
	
	Shift <- FindShifts(P)
	i <- m - 1
	while i<= n-1 do
		k <- 0
		
		// Scan through pattern backwards
		while k <= m-1 and P[m-1-k] = T[i-k] do
			k <- k + 1
		if k = m then
			return i - m + 1
		else
			i <- i + Shift[T[i]]
	
	return -1
```

# Week 7

## Dynamic Programming - Part 1

***In dynamic programming, often solutions to a problem overlap***

### Fibonacci Sequence
0,1,1,2,3,5,8,13,...
```
F(n) = F(n-1) + F(n-2)
F(0) = 1, F(1) = 1
```

If you examine element `i`, we know the solution is the sum of elements `i-1` and `i-2`

```
function Fibonacci(n):
	if n = 0 or n = 1 then
		return 1
	return Fibonacci(n-1) + Fibonacci(n-2)
```


If we computed, for example, `Fibonacci(6)`, we would end up re-computing multiple numbers, as the first step would involve computing `Fibonacci(5)` and `Fibonacci(4)` (And we know that `Fibonacci(4)` is IN `Fibonacci(5)`)

This re-computation can become incredibly expensive, so we can store intermediate solutions.

First allocate and array of size `n` to store previous solutions
```
function DynamicFibonacci(n):
	F[0] <- 1
	F[1] <- 1
	for i = 2 to n do
		F[i] = F[i-1] + F[i-2]
	return F[n]
```

From exponential to linear time complexity.

### Knapsack Problem

Given $n$ items with:
- Weights: $w_1, w_2, ..., w_n$
- Values: $v_1, v_2, ..., v_n$
- Knapsack of capacity $W$

We want to find:
$$max \sum^{n}_{i=0}{v_i}$$

#### Brute-force solution
- Try all possible subset of items, return the most valuable that fits in the backpack
- $\Theta(2^n)$


#### Greedy Algorithm
- Assume items have an arbitrary order
- Add items one-by-one, in order. When an item does not fit, skip it.
- *Not optimal*

#### Optimal:
- Define $F(i, j)$ as the optimal solution for a subset of items $1..i$ and capacity $j$.
- *Case 1*: if item $i$ is not in the optimal solution, then $F(i-1, j)$ 
- *Case 2*: if item $i$ is in the optimal solution, then we need to take into account its weight.
	- The subproblem is the optimal solution for a knapsack of capacity $j-w_i$
	- $F(i,j) = F(i-1,j-w_i) + v_i$

$F(0, j) \ \forall j = 0$
$F(i, 0) \ \forall i = 0$

Express the solution recursively:

$F(i,j) = max(F(i-1, j), F(i-1, j-w_i) + v_i) \ if \ j \geq w_i$
$F(i,j) = F(i-1, j) \ if \ j \lt w_i$

In Fibonacci, we had an array to store solutions
Here, we need a matrix of $n+1$ rows and $W+1$ columns.


## Dynamic Programming - Part 2:

**Applying dynamic programming algorithms to graphs**

**Transitive Closures:**
- Find all node pairs that have a path between them.

The solution to a problem can be broken into solutions to subproblems:
- If there's a path between 2 nodes `i` and `j` which are not directly connected, that path has to go through at least another node `k`. Therefore, we only need to find if the pairs `(i,k)` and `(k,j)` have paths.

### Warshall's Algorithm

In Knapsack, we assume *items* have an arbitrary order
In Warshall's, we assume the *nodes* have an arbitrary order (From 1 to n)

For every pair of nodes `(i,j)` the full problem is: "Is there a path between `i` and `j`?"

This can be interpreted as "is there a path between `i` and `j` that goes through any subset of nodes from `1 to n`?"

This leads to the subproblem: "is there a path between `i` and `j` that goes through any subset of nods from `1 to k`?"


Let $A$ be an adjacency matrix for the graph, and $R$ be a matrix of the same dimension as $A$ that tracks if there is a path from $i$ to $j$. Initially $R^0 = A$, as they begin the same before we account for the new paths we have found to $R$.

When `k=0`, we have the empty subset and $R^0 = A$ .
The goal is to get $R^n$. We can then get the following recurrence:

$$
R_{ij}^{0} = A_{ij}
$$
$$
R^{k}_{ij} = R^{k-1}_{ij} \ or \ (R^{k-1}_{ik} \ and \ R^{k-1}_{kj})
$$

#### Process:
1. Establish adjacency matrix $A = R^0$ for the graph
2. Iterate through the current $R$ matrix, if there is an established connection leave it, if there is no current connection, AND the 2 elements together
(See recursive expression above)

To quickly trace this algorithm on paper, we can mark the $k_{th}$ row and $k_{th}$ column in $R^{k-1}$, and we can add a 1 to $R^k$ to the coordinates where there are are 1s in the $k_{th}$ row and $k_{th}$ column of $R^{k-1}$. (Simply circle the relevant rows and columns and check if there are any 1s in the circles)

For example:
![[Warshall.png]]


Note:
we can use $A$ as $R^k$ to prevent using additional memory (since the algorithm will never overwrite values we need to use)

Warshall's Algorithm is $\Theta(|V|^3)$ in all cases. It's also easily parallelisable

### Floyd's Algorithm

Floyd's Algorithm solves the *all-pairs shortest path* problem for weighted graphs with *positive weights*

Similar to Warhsall's, but uses a weight matrix W instead of adjacency matrix A (with $\infty$ for unknown values)

The update step becomes:
$$ D^k_{ij} = min(D^{k-1}_{ij}, \ D^{k-1}_{ik} + D^{k-1}_{kj}) $$

So we choose the minimum between the previous known path length from `i` to `j` and the sum of the distances to the immediate node (`k`) between `i` and `j`



# Week 8

## Sorting

### Mergesort
```
function Mergesort(A[0..n-1])
	if n > 1 then
		B[0..n/2-1] <- A[0..n/2-1]
		C[0..n/2-1] <- A[n/2..n-1]
		Mergesort(B)
		Mergesort(C)
		Merge(A,B,C)
```

#### Merge Operation:
- Iterate through length of arrays being merged
- If `B[i] <= C[i]`
	- `A[k] = B[i]`
	- `i += 1`
- else
	- `A[k] = C[j]`
	- `j += 1`
- `k += 1`

#### Properties
- Not in-place (requires $\Theta(n)$ sized auxiliary space)
- Stable (maintains relative order if 2 elements are equal)
$$C(n) = 2C(\frac{n}{2})+C_{merge}(n)$$
$C_{merge}$ is a linear function, so $C_{merge}(n) \in \Theta(n) \implies d = 1$
As $a=2$, $b=2$, according to Master Theorem merge sort is $\Theta(nlog(n))$
### Quicksort
```
function Quicksort(A[0..n-1])
	Partition(A)
	Quicksort(left)
	Quicksort(right)
```

#### Partitioning
Lomuto Partitioning

Lomuto Partitioning maintains 3 sections: less than the pivot, greater than the pivot, and unknown.

```
function LomutoPartition(A[l..r])
	p <- A[l]
	s <- l
	for i <- l+1 to r do
		if A[i] < p then
			s <- s + 1
			Swap(A[s], A[i])
	Swap(A[l], A[s])
	return s
```

Process:
- Iterate through the array
- If the current element is smaller than the partition `p`: increment `s` and swap elements at `s` and `i`
- After iteration, swap elements at `l` and `s` and return


Hoare Partitioning

Hoare Partitioning is a 2-pointer approach, where pointers `i` and `j` increment inwards from the left and right bounds respectively, until they both reach an element that should be 'on the other side' of the array, where they swap and continue incrementing until they reach each other. 2 final swaps are done after they meet.

```
function HoarePartition(A[l..r])
	p <- A[l]
	i <- l; j <- r + 1
	repeat
		repeat i <- i + 1 until A[i] >= p
		repeat j <- j - 1 until A[j] <= p
		Swap(A[i], A[j])
	until i >= j
	Swap(A[i], A[j])
	Swap(A[l], A[j])
	return j
```

#### Complexity

Best Case:
$$C_b(n) = 2C_b(\frac{n}{2}) + C_{partition}(n)$$
Worst Case:
$$C_w(n) = 2C_b(\frac{n}{2}) + n + 1$$

#### Properties
- In-place
- Unstable


# Week 9

## Heapsort
Effectively selection sort utilising a priority queue

Overall cost: $C_{heapify}(n) + (n \times C_{eject}(n))$
### Data Structure (The Heap)
A tree with the following properties:
- *Binary* (Two child nodes)
- *Complete* (all levels are full)
- *Parental dominance* (Parent node is greater than child node)

### Top-Down Heapsort
"Bubble Up" Algorithm

$O(nlog(n))$ heapify cost

### Bottom-Up HeapsortG
- Start with the last parent node
- Get the largest child node 
- Check if the largest child is greater than the parent node
```c
void sift_down(int *A, int i, int len) {
	int largest_child_idx = i*2+1;
	
	if(A[largest_child_idx+1] > A[largest_child_idx]) {
		largest_child_idx++;
	}
	
	if(A[i] < A[largest_child_idx]) {
		int temp = A[i];
		A[i] = A[largest_child_idx];
		A[largest_child_idx] = temp;
		
		sift_down(A, largest_child_idx, len);
	}
}

for(int i=len/2; i>=0; i--) {
	sift_down(A, i, len);
	// We now have a max-heap!
}
```

$O(n)$ heapify cost

![[Bottom-Up-Heapsort.png]]
### Heapsort


## Distribution Sort

Specialised non-comparative sorting algorithms.

### Counting Sort
- Only works with non-negative integer keys
- Works best when the key range is small

#### Process:
1. Allocate a `count` array of length `max(A)`
2. Iterate through `A` and log frequencies in `count`
3. Iterate through `count` summing up the counts
4. Subtract 1 from all entries in `count`
5. Allocate output array of length `len(A)`
6. Iterate through `A`, the index in the output array for any given element `A[i]` is given by `count[A[i] - 1]`
7. Decrement the element of the count array that was just referenced

### Radix Sort
- Requires the maximum key length to be known (as we iterate through key digits from least to most significant) 


```
function RadixSort(A[0..n-1], k)
	for j<-0 to len(k) do
		A <- AuxSort(A, k[j])
```

Where `AuxSort` is an auxiliary sorting algorithm (typically counting sort, but can be any *stable* algorithm)

## Binary Search Trees

Binary search trees are an abstract data structure for storing (key, value) pairs

### Dictionary Operations:
- Search
- Insert
- Delete

### General Dictionary Implementations:
- Linked List / Unsorted Array:
	- Search: $\Theta(n)$ comparisons
- Sorted Array:
	- Search: $\Theta(log(n))$ comparisons
	- Insert/Delete: $\Theta(n)$ record swaps
- BST:
	- Search: $\Theta(log(n))$ comparisons
	- Insert/Delete: $\Theta(log(n))$ record swaps


### General Structure:
Smaller keys are on the left, larger keys are on the right

The worst case is when the binary search tree degenerates into a 'stick', this happens when the values are strictly increasing or strictly decreasing 

### Avoiding BST Degeneracy

- Self-balancing Trees
- Changing the Representation

#### AVL Trees (Adelson-Velsky and Landis):
Each node in the BST has a *balance factor* (the difference in height between the left and right subtrees)

When the balance factor becomes 2 or -2, *rotate* the tree to adjust them.

The tree is balanced when:
$$-1 \leq h_L - h_R \leq 1$$

***Rotations:***
R-Rotations:
- When there is a left subtree that is causing the unbalance, we do a right rotation
- We then move everything to the right 1 node

L-Rotation:
- When the right subtree is causing the unbalance
- Move all nodes 1 to the left

LR-Rotation:
 ![[LR-Rotation.png]]
In this case, LR(3) = L(1) + R(3)

RL-Rotation:
![[RL-Rotation.png]]A
In this case, RL(1) = R(3) + L(1)


If there are multiple nodes with balance factor +/- 2, we always choose the LOWEST subtree to be rebalanced

![[General Double Rotation.png]]
T1 and T4 have no 'issues' so they remain in the same place.
T2 is rotating from the left, so it becomes the right node of the child.
T3 is rotating from the right, so it becomes the left node of the child.

