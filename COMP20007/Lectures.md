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

