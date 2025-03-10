
# Objectives:
- Understand the purpose of OO Analysis
- Be familiar with static and dynamic OO models
	- Domain Class Diagrams
		- Identify conceptual classes
		- Create initial domain model
		- Model appropriate attributes and associations
- System sequence Diagrams (SSD)
	- Identify system events

Use cases are fairly high level, we'll now examine a lower level of interaction with the SuD (as far as OOP principles are concerned)


# Week 1 Revisited
Start with *use case diagrams*
From this we can build *use case texts*

This is simply identifying the problem domain and understanding requirements
- Text stories

# Object-Oriented Domain Models

>[!note] Object-oriented Analysis
>Object oriented analysis is a process of creating a description of the domain from the perspective of *object* 

This is still more abstract than *software classes*

OO Analysis includes an identification of the *concepts*, *attributes*, and *associations* that are considered noteworthy in the problem domain.


>[!cite] Definition
>A domain model is a representation of *real-situation* conceptual classes

The domain model is a *Unified Process* (UP) Business Object Model
Visually, we use UML to illustrate a domain model.
- However, we *don't apply any method signatures* or operations
	- We *do have attributes* though
- Interaction specifics are not considered

![[domain-model.png]]

It's important to express relationships between the classes
- e.g. 1 sale has 1 or more line items (and each line item can only apply to a single sale)


## Definitions
- **Conceptual Class**: A conceptual class may be considered in terms of its symbol, intension, and extension (an idea, thing, or object)
	- Symbol: word or images representing the class
	- Intension: The definition of the class
	- Extension: The set of example to which the class applies
- **Association**: A relationship between classes that indicate some meaningful and interesting connection
	- Must be significant
	- Knowledge of the relationship needs to be preserved
	- Derived from the Common Associations List



## Identifying Conceptual Classes

1. Identify based on existing models for common problem domains (e.g. inventory, finance, etc.)
2. Use a category list
3. Identify noun phrases
	- Care must be applied as words in natural languages are ambiguous
	- Do not use as mechanical noun-to-class mapping

>[!example] Category List Example
![[category-list.png]]


### Attributes of Conceptual Classes
Attributes are logical data values of an object.
- Attributes should be included when uses cases suggest the information is important and needs to be remembered


### Subclasses vs. Attributes
We use the generalization/specialization hierarchy when there are significant differences between the objects, otherwise we can just model the difference objects as a single, flexible class.

>[!example] Library Borrowing System Example
>*Subclasses*: Book vs. movie
>*Attributes*: Different user types (only difference is borrow limit)

Subclass must have additional attributes of interest
Subclass has additional associations of interest
Subclass is operated on differently in a noteworthy way

#### Guideline for Creating and Modelling Subclasses

When modelling:
1. Declare superclass abstract
2. Append the superclass name to the subclass


# System Sequence Diagrams

>[!cite] Definition
>A visualisation of the *system events* that external actors generate, the order of the events, and possible inter-system events.

One SSD is for *one particular scenario* of a use case.
The SSD captures dynamic context for the system

![[system-sequence-diagram.png]]

SSDs can also illustrate interactions between systems (like supporting actors)
- **Example**: External credit payment authorizer

Both domain models and SSDs should be expressed at the *abstract level of intention*
- Provide essential abstractions in information required to understand the domain in the context of the current requirements
- Aid people in understanding the domain

