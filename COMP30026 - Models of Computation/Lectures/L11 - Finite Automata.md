
## Example
 An extremely simple example of a finite automata is a *tally counter* that:
 - Displays a *single digit number*
 - Has an *increment button*
 - Has a *reset button*
 
 There are 10 states in this hypothetical scenario representing the numbers 0-9, and can be transitioned between by pressing the buttons.

To convert this transition table into a formal finite automaton (one that receives an input string and either accepts or rejects it), we must make 2 key changes:
- Specify how the device accepts/rejects strings
	- In general, this is done by indicating some states as *accept states*, with the string being accepted if it ends up at one of these
- Specify how transitions between states respond to each incoming bit of the input
	- Need to specify a state transition table

## General Definitions

**Definition 1 - Finite automata for bit strings:**
A finite automaton $M$ consist of:
1. A set of states $Q$
2. Initial state $q_0$
3. State transition function $\delta:Q \times \{0,1\} \to Q$
4. Subset of accept states $F$

**Definition 2 - Alphabet:**
An alphabet is a finite set of "characters" denoted by $\Sigma$


**Definition 3 - Finite automata (generally):**
Same as *definition 1* but with a defined *alphabet* as well.
- The state transition function becomes $\delta : Q \times \Sigma \to Q$

**Definition 4 - Finite automata acceptance:**
A finite automaton $M$ accepts a string $w$ iff $q(w)$ is an accept state.
- The language *recognised* by $M$ is the set of strings accepted by the finite automaton and is denoted by $L(M)$

## Computation Path
The computation path is the series of state transitions undertaken by $M$ for input string $w$

## Key Features
1. Constant memory
	- States and number of states is independent of input length
	- Behaviour depends only on current state and next character
2. Receive the input as a stream
	- Doesn't know when the input is going to end
