

# 1. n-Queens
**1a.**
Row 1: $n$ 
- We can place anywhere

Row 2: $n-2$
- Worst case scenario, previous queen is close to the edge
- Only removes 2 possible positions

Row 3: $n-2-2$
- Need to account for all queens above

....

Row n: $1$


So, the overall number of choices we can make is:
$$n(n-2)(n-4)(n-6)...(1)$$
$$\prod_{i=1}^{\lfloor n/2 - 1 \rfloor}{n-2i} = O(n!)$$

**1b.**
Consider 'iterating' through each row, at each of which we need to decide a column to place a queen in.

Variables: $\{Q_1, Q_2, Q_3,...Q_n\}$ (the queens)
Domains:  $\{1,2,3,...,n\}$           (the possible columns)
Constraints:
- $\cap_{i=1}^{n}{\{Q_i\}} = \emptyset$ (no queens can share a column)
- $\forall (Q_i, Q_j) : i \neq j, |Q_i - Q_j| \neq |i-j|$

**1c.**
```

```


# 2. CSP Heuristics

You pick the most constrained variable because you're likely to discover failures early in the search, preventing unnecessary deeper searching


You pick the least constraining value because, once you have committed to a variable to assign, you want to pick the 'least intrusive' value. i.e. you want the value that is more likely to allow a solution from that state.


# 3. AC-3 Arc Consistency

# 4. AC-Tree
