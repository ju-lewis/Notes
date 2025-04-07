
UML state machines allow us to capture different behaviours based on the 'state' of the program
- i.e. an object may behave differently in different circumstances, which we cannot model clearly with regular UML or Dynamic Design Models

>[!note] Definition
>A state machine is a behaviour model that captures the dynamic behaviour of an object in terms of states, events, and state transitions.
>
>- A *state* is the condition of the object at a moment in time (e.g. idle, active)
>- An *event* is a noteworthy occurrence that affects the object to change state
>- A *state transition* is a directed relationship between two states

![[state-machine-example.png]]


## When/How do we Apply State Machine Diagrams?
Determine the behaviour of an object
- State *dependent* object
	- Reacts differently to events depending on state
- State *independent* object
	- Reacts the same regardless of state
- State *independent* with respect to an event
	- Always responds to an event the same way


**Guideline 1**: Consider state machines for *state-dependent* objects with complex behaviour.
- Model behaviour of complex reactive objects

>[!example] 
>**Complex Reactive Objects**
>- Physical Device Controllers
>- Transactions and related Business Objects
>- Role Mutators
>  
> **Protocols and Legal Sequences**
>- Communication Protocols
>- UI Page/Window Flow, Navigation, or Session
>- Use Case Operation Sequencing


## Transition Actions and Guards

A **transition action** is an action (an object does something) when a transition between states happens
- This may represent the invocation of a method of the class of the state machine

A **guard** is a pre-condition to a transition, i.e., a transition won't happen if the guard is false

## Nested States
A state allows nesting to contain *substates*; a substate inherits the transitions of its superstate (the enclosing state)


