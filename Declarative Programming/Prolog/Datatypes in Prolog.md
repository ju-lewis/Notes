
## Primitives (Atomic Terms):
- Integers
- Floating point numbers
- Atoms

## Variable Terms:
- Dynamically typed
- Can be bound to any other type of term
- Begin with lowercase letter or underscore (if anonymity is desired)

## Compound Terms:
- Analogous to C structs
- Declaration syntax:
	- `functor(arguments)`
	- Example: `card(clubs, 3)`
- Compound terms can have variable-valued arguments
	- These variables are bound through *unification*
	- This is the process of trying to find consistent bindings for all contained variables.