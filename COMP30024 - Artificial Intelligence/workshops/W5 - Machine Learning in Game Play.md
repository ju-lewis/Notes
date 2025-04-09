
# 1.  MENACE

For each state of the game, MENACE stores a list of counters - one counter corresponding to each possible move from the state.

MENACE then picks a move using the counter list as a probability distribution

**1a.**
- There are 9 squares to fill, so we can place 4 of one piece type and 5 of the other

For a given state with $n$ pieces on the board, we can arrange them in $9\choose n$ ways
We then need to 'colour' the pieces, which can be done in $n\choose{\lfloor n/2 \rfloor}$ ways


$$\sum_{n=0}^{9}{9\choose n}{n\choose{\lfloor n/2 \rfloor}}$$


# 2. Monte Carlo Tree Search
**2a.**

>[!Note]
>$C$ is a *black* node, so the victory tally is from *black*'s perspective

- $N(C)$ = total playouts = $24-16=8$

We can easily compute the number of white wins from this node:
- $17-(16-6) = 7$

Hence there are $8$ total playouts from $C$ and $7$ white wins, so there is $1$ black win.
- $U(C) = 1$


**2b.** Computing UCB1 for the nodes of the tree:

| Node | $\frac{U(n)}{N(n)}$ | $\sqrt{\frac{logN(Parent(n))}{N(n)}}$ | UCB1   |
| ---- | ------------------- | ------------------------------------- | ------ |
| B    | $6/16$              | $0.4457$                              | 1.266  |
| C    | $1/8$               | $0.6303$                              | 1.386  |
| D    | $8/8$               | $0.5887$                              | 2.177  |
| E    | $2/2$               | $1.020$                               | 3.039  |
| F    | $0/6$               | $0.5887$                              | 1.1774 |

So, we choose node $E$ for the next playout.


**2c.** Backpropagation
We increment the denominator by 1 for all of the parents of the node the playout was performed from

Depending on whether the white player or black player won we increment the numerator by 1 or 0.

If we were making a playout from a white node and white won, we'd increment white parent node numerators by 1 and black parent nodes by 0.


