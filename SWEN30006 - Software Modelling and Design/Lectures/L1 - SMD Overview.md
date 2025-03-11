
# Why Model and Design Software?

**Modelling**
A software model helps communication, it can be used as a shared artefact to share understanding about a problem

**Design**
Software design should improve simplicity and effectiveness of a software system as well as ease its maintainability

Software is abstract: relationships are not limited by physical proximity.

>[!example]
> **Military Helicopter On-board Software**
> 
> Components:
> - Navigation
> - Weapons Control System
> - Communications System
> - ...
> - Flight Control System (500 KLOC)
> 	- Build1 (150 KLOC)
> 		- Subsystem (15 KLOC - 10% of Build 1, 100 Ada packages)
> 		- Cyclical dependency cluster
> 		- High coupling
> 		- Impossible to maintain
> 		  
> *Lessons*
> - Software complexity is a problem in practice, not just in principle
> - Software developers tend to add complexity when not constrained
> - Requiring developers to think through implications of structure is important
> - These issues are particularly critical in large projects.


# Use Cases
Use cases are a widely used method to discover and record requirements.

They're *text stories* of some actor using a system to meet goals.
- i.e. they describe a use case.
They emphasise the user goals and perspective: "Who is using the system, what are their typical scenarios of use and what are their goals?"

## Terminology
- *SuD*: System-under-discussion
- *Actor*: Something with behaviour, e.g. person, computer system, or organisation
- *Scenario*: A specific sequence of actions and interactions between actors and the SuD
- *Use case*: A collection of related success and failure scenarios that describe an actor using the SuD to support a goal

### Actors
- *Primary Actor*: Has user goals fulfilled through the SuD
- *Supporting Actor*: Provides a service (e.g. information) to the SuD to clarify external interfaces and protocols (e.g. payment provider)
- *Offstage*: Has an interest in the behaviour of a use case (e.g. government tax agency)


Use cases influence many aspects of a software development project
- Design
- Implementation
- Project Management

Use cases are a key source of information for OO analysis and testing
Use cases should be strongly driven by the goals of the project


## Finding a Useful Use Case
**Boss Test**:
- If use case (sequence of tasks) is reported to a boss, would they be happy with the work being done?
	- E.g. not just "logging in"
**Elementary Business Process (EBP) Test**:
- A task performed by one person in one place at one time, in response to a business event, which adds measurable value.
- Leaves data in a consistent state
	- E.g. not just "delete a line item"


![[SWEN30006 - Software Modelling and Design/imgs/use-case-diagram.png]]

