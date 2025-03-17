**Readings**: Larman chapter 15, 16, & 17

OO Design models include:
- Design class diagrams
- Design sequence diagrams

This differs from the content last week about domain models, which are concerned with conceptual classes.

# Analysis, Design, and Implementation

**Domain Models**
- Analysis: An investigation of the problem & requirements
- Emphasises finding and describing objects and concepts in the problem *domain*

**Design Models**
- Design: A conceptual solution to a problem that meets the requirements
- Emphasises defining *software objects* and their *collaboration*

**Implementation**
- Implementation: A concrete solution to a problem that meets the requirements
- Implementation in object-oriented languages and technologies (for an OO-design)


# Object-Oriented Software Design
This is the process of creating a *conceptual solution* by defining *software objects* and their collaboration

**Important Features**:
- Structure and connectedness
	- Levels, including architecture
- Interfaces: methods, data types, and protocols
	- External and internal
- Assignment of responsibilities
	- Principles and patterns

Modelling the conceptual solution:
- Static models: Design class diagram
- Dynamic models: Design sequence diagram

## Layers in OO Design
We focus on the core application logic layer
- OO design of core logic layer similar across technologies
- Essential OO design skills are applicable to other layers
- Other layers tend to be technology/platform *dependent*
	- DB, logging, auth systems, frontend, etc.
- Design approaches/patterns for other layers tends to be technology constrained and changeable

We're going to be focusing on the *application logic layer*
- This is the most platform-agnostic/general layer
- Above is the UI systems, below are the DB/logging systems

## Static Design Models
Representation of software objects which define class names, attributes, and method signatures (but not method bodies)
- Use UML class diagrams to visualise the model

Design class diagram
- Illustrates class names, interfaces, associations, etc.

>[!example] Design Model Example
>![[class-design-model.png]]

Both domain models and design models use UML class notation, but their focuses are different.

>[!cite] Summary
>Domain models **inspire** the design of software objects.
>
>We aim to **reduce the representational gap** between how stakeholders conceive the domain and its representation in software.
>
>![[representational-gap.png]]

**Note**: In UML design models, we can represent derived attributes (i.e. not explicitly stored anywhere) by prefixing the attribute name with a slash "/". Look at the 'total' value above.

### Designing Software Objects

One popular way to design software objects is using **Responsibility-Driven Design** (RDD)

RDD focuses on assigning responsibility to software objects
- Responsibility: The obligations or behaviours of an object in terms of its role

Two types of responsibility:
**Knowing**
- Knowing about private encapsulated data
- Knowing about related objects
- Knowing about things it can derive or calculate
**Doing**
- Doing something itself, e.g. creating an object or doing a calculation
- Initiating action in other objects
- Controlling and coordinating activities in other objects


### Design Class Diagrams to Code
OO Designs provide information necessary to generate the code

OO Design can be mapped to OO programming:
- Attributes -> Java fields
- Method signatures -> Java methods
- Java constructor is derived from the 'create' responsibility

## Dynamic Design Models
This is a representation of how software objects interact via messages
- UML Sequences and Communication diagrams are commonly used to visualise the models

Design sequence diagrams emphasise sequence or time ordering of messages sent between software objects

>[!example]
> ![[design-sequence-diagram.png]]


### System Sequence Diagram vs Design Sequence Diagram

System sequence diagrams treat the system as a black box, focusing on the interaction between actors and the system.

Design sequence diagrams illustrate behaviour within the system, focusing on the interaction between software objects.


![[design-full-example.png]]
