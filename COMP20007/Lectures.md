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

| Notation      | $O(f(n))$                              | $\Omega(f(n))$                         | $\Theta(f(n))$     |
| ------------- | -------------------------------------- | -------------------------------------- | ------------------ |
| Set           | Functions that grow no faster than $f$ | Functions that grow no slower than $f$ | Exact order growth |
| Runtime Bound | Upper (Worst)                          | Lower (Best)                           | Exact              |


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
