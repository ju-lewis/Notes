
**Software Design** is about choosing behaviour and structure of a system
- Planning
- Decomposition based on patterns
**Software Modelling** is the creation of tangible, but abstract, representations of a system
- Different kinds of static and dynamic models


# Unified Process
- Inception
	- Analysis of some use cases
	- Go or no go decision
	- Results in: common vision, use case model (text + diagram)
- Elaboration
	- Discover and stabilise most requirements
	- Start building the *core architecture*, analyse high-risk elements
	- Start thinking about design
	- Results in: Domain and design models for some requirements, software architecture doc (component diagram, factor table, technical memo)
- Construction
- Transition

## Inception
### Use Cases
- Write use case texts *first*
- Remember use case models are extremely simple
	- Actors have arrows drawn directly to use cases
	- Primary actors on the left, supporting actors on the right

>[!Info] Possible Exam Question
>Given a use case text, draw a use case diagram

Remember the tests for use cases:
- Boss test (would the boss be happy with the time spent on the task)
- EBP (does the use case generate 'business value')

Use case diagrams can also have *include relationships*
- Used for 'special cases' that aren't strictly a unique use case
There are also *extend relationships*


## Elaboration
### Domain Model
- Capture the concepts attributes, and associations in the domain
- **Domain class diagram**
	- Remember not to think about solutions at all! We're just describing the problem space
- **System sequence diagram**
	- How actors interact with the system
		- Literally lines between the *actor* and *system*
		- Anything referenced in the SSD should be in the static domain model
	- Lines are annotated with pseudo-method-calls
- **Domain state machine**
	- Capture dynamic behaviour in the domain in terms of states, events, and transitions

### Architectural Analysis
>[!cite] Definition
>An activity to identify *factors* that will influence the architecture, to understand their variability and priority, and resolve them.

**Goal**: Reduce risk of missing a critical factor in the design of a system
- Both functional and non-functional architecturally significant requirements

#### Architectural Factor Tables
Architectural factor tables are like requirement tables for the architecture
- e.g. Feature: reliability (recoverability of POS), requirements, risk, priority, etc.
#### Technical Memos
Details specific solution for architectural requirements
- Also specify **unresolved issues** (ideally there should be none) and **alternative solutions** considered

### Design Model
- Mirror the domain model at a tangible representation of software classes to illustrate the structure, collaboration, and responsibilities of software objects
	- Design class diagram
	- Design sequence diagram
	- State machine diagram
- Use a responsibility-driven design: GRASP and GoF design patterns
	- (See previous lecture notes on these)



# Exam Information
2x double sided A4 pages of notes allowed
- Can be hand written *or* printed

The exam will have:
- MCQ
- Short answer
	- /Long answer
- Diagramming
In that order

>[!Note]
>There is likely to be sections interpreting Java code snippets
>There may be short code writing sections
>- They're not going to be looking for *perfect* syntax, so long as it's logical




