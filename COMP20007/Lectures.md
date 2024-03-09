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


### Asymptotic Analysis
We are interested in *growth rate* of functions:
- ignore constant factors
- Ignore small input sizes

$$ f(n) \prec g(n) \iff \lim_{n->\infty}\frac{f(n)}{g(n)}=0$$


### Big-Oh Notation

We write $t(n)\in O(g(n))$ when, for some $c$ and $n_0$,

$$n > n_0 \implies t(n) < c \cdot g(n)$$
*For any constant $n$, there is a multiple of $g(n)$ that is greater than $t(n)$*

For example,
$$ 1 + 2 + ... + n = \frac{(n+1)n}{2} \in O(n^2) $$


### Big-Omega and Big-Theta

$\Omega(g(n))$ denotes the set of functions that grow **no slower than $g$**, so $\Omega$ is for *lower* bounds. (So the big-omega notation of a function means the algorithm will always take longer to execute than $g(n)$  )


$\Theta(g(n))$ is for *exact* order growth.

