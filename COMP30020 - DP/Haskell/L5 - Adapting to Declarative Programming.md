

Remember to compile with `-fwarn-incomplete-patterns`


### Reliability
We can easily create auxiliary functions that are self-documenting through the type system and code structure

We should document these auxiliary functions as regular functions (they should remind the reader of their tasks)

The description should allow readers to construct a correctness argument from the function


### Productivity
There is typically a higher effort required to write and properly document a declarative function. This effort is easily payed off by:
- Other members needing to read the code
- The original author needing to read the code later on


### Efficiency
Declarative programs are typically less space efficient (due to stack frame allocation)

Overall declarative languages are typically slower than they would if they were written in C. Sometimes this slowdown can be small (~10%) up to 100s of times slower.

The right point on the productivity vs efficiency tradeoff continuum depends on the project.


## Declarative Thinking

Some problems are difficult to approach imperatively

The imperative approach is procedural: we devise a way to solve the problem step by step


The declarative approach breaks down the problem into chunks (functions), assembling the results of the chunks to construct the result.

You must be careful in imperative languages, chunks may not compose due to side-effects.


**Recursive Thinking**:
- Determine how to produce the result for the whole problem from the results for the parts of the problem (recursive case)
- Determine the solution for the smallest part of the input (base case)


### Immutable Data Structures

What if you need to update a data structure?
	You create a new one with the change made







