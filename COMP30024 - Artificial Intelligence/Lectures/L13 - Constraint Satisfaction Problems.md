
So far, with standard search problems each state is a *black box* 
- We can use any data structure that supports `GoalTest`, `Eval`, `Successor`

In **Constraint Satisfaction Problems (CSP)**:
- state is defined by *variables* V, with values from *domain* D
- Goal test is a set of *constraints* specifying allowable combinations of values for subsets of variables


>[!Example] Example - Map Colouring (Australian States and Territories)
>**Variables**: WA, NT, Q, NSW, V, SA, T
>**Constraints**: Adjacent regions must have different colours, e.g. WA $\neq$ NT (if the language allows this), or $(WA, NT) \in \{(red,green), (red,blue),...\}$


## Constraint Graphs

*Unary Constrains*: Each constraint involves 1 variable
*Binary Binary Constraints*: Each constraint relates 2 variables
*Higher order constraints*: Constraints involve 3 or more variables
*Preferences* (soft constraints)
- e.g. red is better than green
- Often representable by a cost for each variable assignment
- Constrained optimisation problems


### Discrete Variables
Finite domains; size d $\implies O(d^n)$ complete assignments
where $n$ is the number of variables in the CSP
- e.g. Boolean CSPs, incl. boolean satisfiability (NP-complete)
- e.g. job scheduling, where variables are start/end days for each job
- Needs a *constraint language*
- *Linear* constraints solvable, *non-linear* constraints are undecidable

### Continuous Variables
- e.g. Start/end times for Hubble Telescope observations
- Linear constraints are solvable in polynomial time by *linear programming* methods


>[!Example] 
>Given this cryptarithmetic problem, assign a different value (0-9) to all variables such that the addition is true.
>![[CSP-problem-example.png]]
>
>We can form the *constraint graph*:
>![[Screenshot 2025-04-16 at 4.40.13 pm.png]]
>
>**Constraints**:
>- All different (this it the top square that reaches all variables)
>- Each digit of the sum result is a constraint (which relates the 2 digits above it and any addition carryover from the previous digits)


Real world CSPs typically involve real-valued variables
- Assignment problems
- Timetabling problems
- Hardware configuration
- Floorplanning
- Factory scheduling


## Applying Standard Search

States are defined by the values assigned so far
- *Initial State*: the empty assignment $\emptyset$
- *Successor Function*: assign a value to an unassigned variable that does not conflict with current assignment
	- Fails if no legal assignments
- *Goal Test*: Check that assignment is complete

Every solution will appear at depth $n$ if there are $n$ variables
- Hence, we should use depth-first search
- The path is irrelevant, so we can use complete-state formulation

**Complexity**:
- $b=d(n-l)$ at depth $l$ (because we've assigned $l$ variables)
	- Results in $n!d^n$ leaves!!


## Backtracking Search

Variable assignments are commutative, i.e. it doesn't matter when we assign variables.


```
function BacktrackingSearch(csp) return solution/failure
	RecursiveBacktracking({}, csp)
end

function RecursiveBacktracking(assignment, csp)
	if assignment is complete then
		return assignment
	end if
	var <- SelectUnassignedVariable(Variables[csp], assignment, csp)
	foreach value in OrderDomainValues(var, assignment, csp) do
	
		if value is consistent with assignment given Constraints[csp] then
			add {var = value} to assignment
		end if
		
		result <- RecursiveBacktracking(assignment, csp)
		if result != failure then
			return result
		end if
		remove {var = value} from assignment
	return failure
end
```

