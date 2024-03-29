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