
# Game Playing

**Games vs. search problems**
- "Unpredictable" opponent -> solution is a contingency plan
- Time limits -> unlikely to find goal, must approximate


## Types of Games

Perfect information -> we can observe the entire state of the game

|                       | Deterministic                | Chance                   |
| --------------------- | ---------------------------- | ------------------------ |
| Perfect Information   | Chess, checkers, go, othello | Backgammon, monopoly     |
| Imperfect Information | Battleships                  | Bridge, poker, scrabble, |

## Representing a Game as a Search Problem

We can formally define a *strategic two-player game* by:
- Initial state
- Actions
- Terminal test (win/lose/draw)
- Utility function (i.e. numeric reward for outcome)
	- Chess +1, 0, -1
	- Poker: cash won or lost

In a zero-sum game with 2 players:
- Each player's utility for a state are equal and opposite


# Strategies


## Minimax
Perfect play for deterministic, perfect-information games

>[!note] Idea
>Choose move to position with highest *minimax value*
>- Best achievable payoff against best play

**Note**:
- This assumes the opponent is performing perfect play


### Example:

Consider a "1-shot" game, where each player can make 1 move and the outcome is decided.

The minimax strategy considers the possibilities for both players.
- Take into account that we are trying to maximise our utility ("payoff")
- Opponent is trying to minimise our utility

We make the first decision (e.g. either A1, A2, or A3)
- The utility of our decision is determined by the *minimum* value of the possible outcomes
- This is because a perfect opponent will try to *minimise* the *maximum* value we can obtain

>[!example] 2-Ply Game Example
> ![[minimax-tree.png]]
> 
> **Note**:
> - The upwards arrows indicate it's our turn
> 	- (Maximising layer)
> 	- We can choose to take the greatest value from the child branches
> - Downwards arrows indicate opponent's turn
> 	- (Minimising layer)
> 	- Assume the opponent will take the minimum value from the child branches


### Minimax Algorithm

```
function MinimaxDecision(game) return an operator
	for each op in Operators(game) do
		Value[op] <- MinimaxValue(Apply(op, game), game)
	end
	return op with the highest Value[op]


function MinimaxValue(state, game) returns a utility value
	if TerminalTest[game](state) then
		return Utility[game](state)
	else if Max is to move in state then
		return highest MinimaxValue of successors(state)
	else
		return lowest MinimaxValue of successors(state)
```


### Minimax Properties

Minimax somewhat resembles *depth-first search*
- A given game state is only concerned with its successors

**Complete**: Yes, if tree is finite
**Optimal**: Yes, against an optimal opponent
**Time Complexity:** $O(b^m)$
**Space Complexity:** $O(bm)$ (depth-first exploration)

For chess, $b \approx 35, m \approx 100$ for "reasonable" games
 - Exact solution completely infeasible


## Resource limits

Suppose we have 100 seconds, explore 10^4 nodes/second
- 10^6 nodes per move


Standard approach:

**Cutoff test**
- E.g. depth limit
- Perhaps add quiescence search

**Evaluation Function**
- Estimated desirability of position

>[!example] Chess Example
>Typically for a game like chess, we would use a *linear* weighted sum of features
>- Stock
>- Check
>- Board control

