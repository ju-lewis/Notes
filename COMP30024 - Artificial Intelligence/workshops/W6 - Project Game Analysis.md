

# 1. State Space Analysis

From a given position the maximum number of possible reachable states is:
- +1 grow action
- 6 frogs \* 5 directions = +30 single-jump moves
- The longest multi-jump sequence is 11 jumps (assume all 6 frogs can make this multi-jump)
	- For each step along the multi-jump we can stop, so the number of possible moves added is $6 \times \sum_{i=1}^{11}i$



