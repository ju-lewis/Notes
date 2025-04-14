
**Types of patterns**
- Creational Patterns
	- Abstract instantiation process
- Structural Patterns
	- Describe how classes and objects can be combined to form larger structures
	- Provides a way to *define relationships* between classes or objects
- Behavioural Patterns
	- Are most specifically concerned with communication/interaction between objects


# Facade Pattern

>[!Warning] Problem
>Require a common, unified interface to a disparate set of implementations or interfaces - such as within a subsystem - is required. There may be undesirable coupling to many objects in the subsystem

Consider a situation in which we want *"pluggable business rules"* in a point-of-sale system that define when to invalidate a transaction.
- Paying by gift card
	- Allow one item to be purchased -> invalidate subsequent `enterItem` requests
- Charitable donation (by store) sale
	- Invalidate `enterItem` requests for values greater than $250
This customisation should have *low impact* on the existing software components


Need to be able to define rules which can be checked
So we need a *rule engine* subsystem, implementation not yet known. Some implementations could be:
- Strategy pattern
- External business rule checker
- Library
- etc.

We don't want our code to have high coupling with the system implementing the rule checking, we just want a single objects that exposes a simple unchanging interface to the POS system.



**Solution**:
Define a single point of contact for the subsystem. A *facade object* that 'wraps' the subsystem.

![[facade-pattern.png]]

In the POS example, we'd define a class: `public class POSRuleEngineFacade`
that acts as a singleton and exposes `isInvalid(Payment, Sale)`, `isInvalid(SalesLineItem, Sale)`
- Now our POS system doesn't care about how the rules are actually checked


# Decorator Pattern

>[!Warning] Problem
>You want to dynamically add behaviour to *individual objects* at run-time without changing the interface presented to the client.

We can't use interfaces here because they are static and apply to the entire class.

**Solution:**
- Encapsulate the original concrete object inside an abstract wrapper interface. Then, let the *decorators* that contain the dynamic behaviour also inherit from this abstract interface. The interface will then use *recursive composition* to allow an unlimited number of decorator "layers" to be added to each object.

![[decorator-pattern.png]]
A client is always interested in `ConcreteComponent.operation()` but *may or may not* be interested in `ConcreteDecorator.operation()`

The `Decorator` class must expose the underlying behaviour of the component, and can be extended by `ConcreteDecorator`s to modify (*decorate*) the behaviour
- When we call the underlying function defined by the component, it'll make calls to all of the decorators, because we continue to 'wrap' the component in decorator classes.


# Builder Pattern

>[!Warning] Problem
>How can a class (the same construction process) create different representations of a complex object?
>How can a class that includes creating a complex object be simplified?


**Solution**:
Encapsulate creating and assembling the parts of a complex object in a separate `Builder` object. A class delegates object creation to a `Builder` object instead of creating it directly.

A `Client` makes a simple request to a `Director`, the `Director` contains an abstract `Builder` class that defines the process of creating the objects (e.g. juice).
- We simplify the object creation by making them conform to the structure defined in an abstract class, so the director only needs to know about the abstract class's interface.
- This simplification is where the Builder Pattern differs from just directly specifying the creation process in the `Director` class. It's all about abstraction.

![[builder-juice-example.png]]


