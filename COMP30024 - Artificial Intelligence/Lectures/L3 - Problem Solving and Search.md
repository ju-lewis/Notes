
# Problem-Solving Agents

Restricted form of a general agent:
```
function simple_problem_solving_agent(p) return an action
	inputs: p, a percept
	static: s, an action sequence (initially empty)
			state, some description of current world state
			g, a goal
			problem, a problem formulation
	state <- update_state(state, p)
	if s is empty then
		s <- formulate_goal(state)
		problem <- formulate_problem(state, g)
		s <- search(problem)
	action <- recommendations(s, state)
	s <- remainder(s, state)
	return action
```

**Note**: this is *offline* problem solving

*Online* problem solving involves acting without complete knowledge of the problem and solution.


>[!example]
>## Holiday in Romania 
>
>An agent is currently in Arad. Their flight leaves tomorrow from Bucharest.
>
>1. **Formulate Goal**: Be in Bucharest
>2. **Formulate Problem**: `states`: various cities, `operators`: drive between cities
>3. **Find Solution**: Sequence of cities


## Single-State Problem Formulation
A single-state problem is a problem where we can clearly observe what state we are in (as opposed to partially observable environments)

A problem is defined by **four items**:
- *Initial state* - e.g. "at Arad"
- *Actions* (or successor function $S(x)$) - e.g. Arad $\rightarrow$ Zerind, Arad $\rightarrow$ Sibiu, etc.
- *Goal Test* - explicit, e.g. $x$ = "At Bucharest" implicit, e.g. "Checkmate" in chess
	- An explicit goal state is an exact description of a state
	- An implicit goal state satisfies some sort of 'goal test'
- *Path Cost* (additive) - e.g. sum of distances, number of actions executed, etc.

>[!note]
>"actions" = "operators"

### Selecting a State Space
Real world is absurdly complex
- State space must be *abstracted* for problem solving

(Abstract) state = set of real states
(Abstract) action = complex combination of real actions
(Abstract) solution = set of real paths that are solutions in the real world

>[!example]
>Abstract state "in Arad" corresponds to the real world state of being *somewhere* in the city of Arad (e.g. at hotel, petrol station, public park)

Each abstract action should be "easier" than the original problem!


States: Positions of all tiles on the board; e.g. (5, (1,2))
Actions:  move tile adjacent to 'gap' into the 'gap'
- Possibly up,down,left,right
Goal test: Board arranged in goal state
Path cost: Moves made


# Search Algorithms

Basic idea:
- Offline, simulated explorations of state space by generating successors of already-explored states
	- a.k.a. *expanding* states

```
function general_search(problem, strategy) returns a solution, or failure
	initialise the search tree using the initial state of problem
	loop do
		if there are no candidates for expansion then
			return failure
		choose a leaf node for expansion according to strategy
		if the node contains a goal state then
			return corresponding solution
		else
			expand the node and add the resulting nodes to the search tree
	end
```


## Implementation

A *state* is a representation of a physical configuration
A *node* a is a data structure constituting part of a search tree
- Contains additional information about parents, children, path costs, etc.

The `expand` function creates new nodes, filling in various fields and using `operators` (or `actions`) of problem to create the corresponding states


### General Search algorithm implementation
```
function general_search(problem, queueing_fn) returns a solution or failure
	nodes <- make_queue(make_node(initial_state[problem]))
	loop do
		if nodes is empty then return false
		node <- remove_front(nodes)
		if goal_test(problem) applied to state(node) succeeds then
			return node
		nodes <- queueing_fn(nodes, expand(node, operators(problem)))
	end
```


