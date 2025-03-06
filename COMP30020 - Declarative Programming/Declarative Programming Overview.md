
## Side Effects
Code has a side effect if, in addition to producing a value, it also modifies some state or has an observable interaction with calling functions or the outside world.

**Examples:**
- Modify global/static variable
- Modify an argument
- Raise an exception
- Write data
- Read data
- Call other side-effecting functions


### Destructive Updates
In imperative languages the natural way to insert a new entry into a table is to modify the table in-place. In declarative languages, you instead create a new version of the table

The cost is that the language implementation has to work harder to recover memory.

Immutability of data structures greatly improves the ability to parallelise.
