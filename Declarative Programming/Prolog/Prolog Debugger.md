
## Byrd Box Model

The Prolog debugger operates on the Byrd Box Model:
1. Execution of a predicate will initially enter through the `Call` *port*
2. Execution failure causes a return through the `Fail` *port*
3. Execution completion (success) returns through `Exit` *port*
4. If a goal after a nested choice point fails, it re-enters through `Redo` *port*

