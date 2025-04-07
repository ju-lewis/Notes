
MCTS abandons the use of complete search using a cut-off depth and an evaluation function

Instead, MCTS estimates the *average utility* of a state by playing multiple games from that state all the way to a *terminal state* of the game using an *initial move selection policy*

The value of the state is then estimated from the average of the outcomes of those games (rather than using a heuristic evaluation function)

Each game that is played from a state to a terminal state is called a *playout* or *simulation*.
- Each simulation runs in linear time! (It's *NOT* a search :D)

>[!summary]
>MCTS replaces an evaluation function with an average of psuedo-random estimates based on playing the game!


## Playout Policy
How do we decide what moves to make during a playout?
- Random moves -> will learn very slowly
- Game specific heuristics -> based on expert knowledge
- Learned evaluation function based on self-play -> Guides search during playout; but the outcome of the playout is based on the terminal state, not the evaluation function

If we can sample enough playouts, we can measure the average utility of a state, rather than rely on a heuristic function to "guess" the state's utility


## MCTS - Key Steps
We gradually expand the search tree using the following four steps:
- **Selection** - Starting from the root of the tree, use a selection strategy to choose successor states until we reach a leaf node of the tree
- **Expansion** - From the selected leaf node, expand the node by adding to the tree a single new child from that leaf node
- **Simulation** - Perform a playout from the newly added node to a terminal state, but don't add the moves/states explored in the playout to the search tree
- **Backpropagation** - Use the outcome from the playout (win/loss) to update the statistics of each node from the newly added node back up to the root

```
function MCTS(state) returns an action
	tree <- Node(state)
	while isTimeRemaining() do
		leaf <- Select(tree)
		child <- Expand(leaf)
		result <- Simulate(child)
		BackPropagate(result, child)
	return the move in Actions(state) whose node has the highest number of payouts
```

>[!example] 
>In this example, the 'search frontier' has been expanded a few moves ahead
> ![[mcts-example.png]]
> We continue to expand nodes as we playout from new states


## MCTS Comments

- Complexity of a playout is linear in the depth of the tree, not exponential
- We can perform a huge number of playouts in the time it would take $\alpha-\beta$ search to look a few moves ahead
- Playouts allow use to learn from the actual outcome of a game, rather than using a heuristic
- By focusing on moves that have a high win rate, but still allowing some flexibility to explore other moves


## Selection Policy

A selection policy we can use from reinforcement learning theory is called *upper confidence bound applied to trees*, and has the formula $UCB1(n)$  for a node $n$


$$UCB1(n) = \frac{U(n)}{N(n)} + C\times \sqrt\frac{\log N(\text{Parent}(n))}{N(n)}$$
**Where**
- $U(n)$ - total utility (e.g. number of wins) from all playouts through node $n$
- $N(n)$ - total number of playouts through node $n$
- $\text{Parent}(n)$ - Parent node of $n$ in the tree
- $C$ - a constant that balances *exploitation* with *exploration*

When choosing between sibling nodes, select the node with the highest $UCB1$ value. If a node has few playouts compared to the parent, then the second term will be larger



# Summary
- Discuss opportunities for learning in game playing
- Trace MCTS for a game
- Explain the difference between exploitation and exploration



