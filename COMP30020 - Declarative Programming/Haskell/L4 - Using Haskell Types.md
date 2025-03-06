
Comparing representations between languages


Adding new type to a union/compound type
**Java**
- Add new class implementing all methods

**C**
- Add new alternative to enum
- Add members to the type
- Add code to functions to handle enum

**Haskell**
- Add a new alternative - with arguments - to the type
- Add code for it to all functions handling the type
	- New equation/case


Adding a new operation:
**Java**
- Adding a new method to parent class
- Implement it for all subclasses

**C**
- Write one new function 

**Haskell**
- Write one new function


## Switching on Alternatives
You don't need separate equations for each possible *shape* of the arguments.

The following function checks whether the value of an expression (`Expr` type) can be known statically
```haskell
is_static :: Expr -> Bool
is_static expr = 
	case expr of
		Number _     -> True
		Variable _   -> False
		Unop _ expr1 -> is_static expr1
		Binop _ expr1 expr2 -> 
			is_static expr1 && is_static expr2
```


