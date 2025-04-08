
# Indirection

**Problem**: Where to assign a responsibility to *avoid direct coupling*  between two (or more) things?
- How to de-couple objects so that low coupling is supported and reuse potential remains higher?

**Solution**:
Assign responsibility to an intermediate object to mediate between other components or services so that they are not directly coupled.
- The intermediary creates an *indirection* between the other components

>[!example] POS Example
>
>In a point-of-sale system, taxes are calculated by an external service `TaxMasterService` accessed over TCP. If we go by the [[L4 - Responsibility Driven Design#Information Expert (or Expert)|information expert]] principle, we would attribute the TCP interface code to a `Sale` class, which contains information about the transaction.
>
>This however, has the issue that all instances of Sale now individually interface with the TCP logic - which is quite a high level of unnecessary coupling. We can create a `TaxMasterAdapter` class to interface between the two.
>

## Discussion

The motivation for indirection is usually Low Coupling (i.e, decouple objects for future reuse)

Old adage:
	"Most problems in computer science are solve by another level of indirection."

There is however, a performance overhead associated with indirection.


# GRASP Patterns Continued

## Pure Fabrication

**Problem**: which object should have responsibility when you do not want to violate *high cohesion* and *low coupling*, but solutions offered by other patterns are not appropriate?
- Domain model often inspires the design of software objects (achieving low representational gap)
- In many situations, assigning responsibilities only based on the domain model often leads to the problem of poor cohesion or coupling.

**Solution**: Assign a highly cohesive set of responsibilities to an *artificial* or "convenience" class created to maintain good design principles.

>[!example] Monopoly Example
>
>Who should be responsible for rolling the dice?
>
>If we assign responsibility according to the *information expert principle*, we'd assign it to the `MonopolyGame` class. This however, would eventually lead to the issue where everything is done in the `MonopolyGame` class, defeating the purpose of object oriented design. (**Very low cohesion**)
>
>
>**Solution**: We can solve this using *pure fabrication*, by creating an artificial class called `Cup` that exposes `roll` and `getTotal` methods.
>
>Now both `Player` and `MonopolyGame` have simple interfaces with the `Cup` class, and it prevents everything from being computed in a single class.
>

### Contraindications
Many pure fabrications are generated because of indirection:
- Assigning any class as an intermediary

Pure fabrication *should not* be used as an excuse for adding new objects.

If overused, pure fabrication can lead to the design having classes with one responsibility
- Can eventually adversely impact coupling


## Polymorphism

**Problem 1**: How do we handle alternatives based on type?
- Conditional variation: adding new alternatives and if-then-else are required in many places.

**Problem 2**: How to create pluggable software components?


We shouldn't be manually testing types for alternative behaviour, rather we should use the mechanisms of the language to express the types.

### Discussion
Polymorphism is a fundamental pattern in designing how a system is organised to *handle similar variations*
- Based on polymorphism, a design is easily extended to handle new variations

### Contraindications
- Designing systems with interfaces and polymorphism for speculative "future-proofing" against an unknown variation could be useful
- However, unnecessary effort might occur if polymorphism is applied at all locations where variation could possibly arise (which it often doesn't).


## Protected Variation
**Problem** How to design objects, subsystems, and systems, so that the variations or instability in these elements do not have an undesirable impact on other elements

Points of change include:
- Variation point: Variation in existing system or requirements
- Evolution point: Speculative variations that may arise in the future.

**Solution**:
- Identify points of known or predicted variation or instability


>[!example] POS Example
>
>Need to consider possible instability of `TaxMasterSystem`, e.g. what if we need to change to a library that exposes an API for computing tax instead of a TCP socket?
>
>We can use polymorphism and protected variation to allow use of multiple adapters in the future - hiding behind a stable interface.



