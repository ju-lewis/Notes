
Many design decisions need to be fine-tuned in game playing agents
- Can we automatically tune these decisions?

We can use:
- Search control learning
- Monte Carlo tree search

**Challenges in Game Agent Design**

Handling each stage of the game separately:
- Compile a "book" of opening games or end games

Adjusting search parameters:
- Search control learning

Adjusting weights in evaluation functions
Finding good features for evaluation functions



## Book Learning

>[!note] Aim
>Learn a sequence of moves for important positions

**Example 1**: In chess, there are books of opening moves
- For every position seen in an opening game, remember the move taken and the final outcome
**Example 2**: Learn from mistakes
- Identify moves that lead to a loss


## Search Control Learning

>[!Note] Aim
>Learn how to make search more efficient

**Example 1**: Order of move generation affects $\alpha-\beta$ pruning
- Learn a preferred order for generating possible moves to maximise pruning of subtrees

**Example 2**: Can we vary the cut-off depth?
- Learn a classifier to predict what depth we should search to based on current state


## Learn Evaluation Function Weights

>[!Note] Aim
>Adjust weights in evaluation function based on experience of their ability to predict the *true final utility*

**Recall:**
- Typically use a *linear weighted sum* of features

### Supervised Learning

In the case of learning the weights of an evaluation function, the training example corresponds to the set of features of a state $s$, with the true minimax utility value of the state as desired output:
- Features = recorded attributes of state $s$
- Ground truth = minimax utility value

$$\text{Eval}(s) = \vec{w}\cdot \vec{f_s}$$

**Problems**
- Delayed reinforcement:
	- Reward result from an action may not be received until several time steps later, which also slows down the learning
- Credit assignment:
	- It's hard to attribute the outcome/utility to any given move


### Temporal Difference Learning
Supervised learning is for single step prediction
- E.g. predict Saturday's weather based on Friday's weather

Temporal Difference (TD) learning is for multi-step prediction:
- e.g. Predict Saturday's weather based on Monday's weather, then update prediction based on Tue's, Wed's, etc.
- predict outcome of game based on the first move, then update prediction as more moves are made


Correctness of prediction not known until several steps later

Intermediate steps provide information about correctness of prediction

TD learning is a form of *reinforcement learning*

#### TDLeaf($\lambda$) Algorithm

Combines temporal difference learning with minimax search

Basic idea: update weight in evaluation function to reduce differences in rewards predicted at different levels in search tree
- Good functions should be stable from one move to the next

# Monte Carlo Tree Search

**Motivation**: In some games, it can be hard to find a good evaluation function

For example, in Go the material value of the pieces on the board is not a good predictor of the outcome from a state
- Also, the positions of the pieces can change considerably throughout the game
- The branching factor is so high that even $\alpha-\beta$ pruning can only look a small number of moves ahead

Monte Carlo Tree Search (MCTS) was invented as an alternative approach *as it does not depend on a heuristic evaluation function*.



