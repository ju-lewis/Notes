
# Adapter Pattern

>[!Warning] Problem
>How to resolve incompatible interfaces, or provide a stabled interface to similar components with different interfaces?

**Solution**
- Convert the original interface of a component into another interface, through an intermediate adapter object.


Consider a situation where a POS system needs to support several kinds of external services, including:
- Tax calculators
- Accounting systems
- Credit authorisation systems

Each service has a different API, which cannot be changed.


>[!Note] Adapter vs. Facade
>The *facade* pattern involves creating a new interface that simplifies a set of complex operations (and reduces coupling).
>
>The *adapter* pattern involves converting one (or more) external interfaces into a single expected interface

For each external system we interact with, we define an adapter.


## Issues arising from Adapter
- Who creates the adapter?
- Which class of adapter should be created?

*Partial answer*:
- Separation of concerns/high cohesion

# Concrete Factory Pattern
*AKA Simple Factory*

>[!Warning] Problem
>Who should be responsible for creating objects when there are special considerations, such as complex creation logic or desire to separate concerns?

**Solution**:
- Create a Pure Fabrication object called a Factory that handles creation.

## Advantages
- Separate responsibility of complex creation into cohesive helper objects
- Hide potentially complex creation logic
- Allow introduction of performance-enhancing memory management strategies
	- e.g. object caching or recycling, connecting to a database many times


## Issues
- Who creates the factory and how is it accessed?
- Oftentimes only one instance of the factory is needed

*Answer*:
- Make the factory a *singleton*

# Singleton Pattern

>[!Warning] Problem
>How do we ensure there is only one instance (a singleton) of a class with a global point of access?


**Solution**
- Define a static method on the class that returns the singleton instance.

`getInstance()` will:
- Check if the private static `instance` reference is null
- Null? -> Create new instance, set the static attribute, and return reference
- Non-null? -> Return the `instance` attribute value


>[!Note]
>Use `synchronized` modifier on the `getInstance` method to prevent race conditions.

Not all attributes and methods on the singleton class are static because we may want to perform overriding on subclasses, which isn't possible with static methods.

Also, a class is not always a singleton in all contexts





