**Readings**: Larman chapter 17

# RDD Revisited 
RDD focuses on assigning *responsibility* to software objects
- Obligations or behaviours of an object in terms of its role
Two types of responsibility:
- Knowing
- Doing


# GRASP
>[!note] Definition
>**G**eneral **R**esponsibility **A**ssignment **S**oftware **P**atterns/**P**rinciples
>
>A set of patterns (or principles) of assigning responsibilities into an object
>

GRASP aids in applying design reasoning in a methodical, rational, and explainable way
- Given a specific category of problems, GRASP guides responsibility assignment

Patterns are repeatable problem-solution pairs to common problems in software development

## Advantages of Patterns
- Capture expertise and make it accessible to non-experts in a standard form
- Facilitate successful applications of expertise
- Improve understandability
- Facilitate communication among practitioners by providing a common language
- A new solution can be generated based on a modified version of existing patterns


## Some Patterns:

### Creator Pattern
**Problem:** Who should be responsible for *creating* a new instance of class A?
- Creation of objects is one of the most common OO activities
- Useful for lower maintenance and higher opportunities for reuse (low coupling)

**Solution**: Assign *class B* responsibility for creating instances of *class A* if one or more of the following is true:
- B "contains" or compositely aggregates A
- B records A
- B closely uses A
- B has the initialisation data for A

>[!example] Monopoly Simulation
>Who should be responsible for creating the 'Square' object?
>
>Solution:
>- The 'Board' object contains the 'Square's
>- The 'Board' records the 'Square's
>- Both 'Board' and 'Piece' closely use 'Square'
>- Initialisation data is N/A

#### Contraindications
If creation of objects has significant complexity, e.g.
- Using recycled instances for performance
- Conditionally creating and instance from one of a family of similar classes

It is advisable to delegate creation to a helper class called a *Concrete Factory* or an *Abstract Factory* rather than use the class suggested by Creator


### Information Expert (or Expert)
**Problem**: What is a general principle for assigning responsibilities to objects?
- Given object X, which responsibilities can be assigned to X?

**Solution**: Assign the responsibility to object X if X has the information to fulfill that responsibility
- Information Expert is useful for understandability, maintainability, and extendibility

>[!example] POS Example
>Who should be responsible for calculating *Subtotal*?
>
>**Approach**
>- What info do we need for the subtotal?
>- Where is the requisite information stored?
