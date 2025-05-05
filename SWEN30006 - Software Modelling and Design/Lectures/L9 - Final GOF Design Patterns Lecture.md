
# Strategy Pattern

>[!Warning] Problem
>How to design for varying, but related, algorithms or policies?
>How to design for the ability to change these algorithms or policies?

**Solution**:
- Use polymorphism to design a single interface (`Strategy`) that exposes a function that all algorithms/policies must implement
	- The classes that implement this interface are called `XYZStrategy` where `XYZ` is the specific policy/algorithm they represent 


**Example**:

```java
public interface ISalePricingStrategy {
	public double getTotal(Sale S);
}

public class AbsoluteDiscountOverThresholdPricingStrategy
implements ISalePricingStrategy {
	public double getTotal(Sale s) {
		....
		return total;
	}
}
```

# Composite Pattern

>[!Warning] Problem
>How to treat a group or composition structure of objects the same way (polymorphically) as a non-composite (atomic) object?

**Solution**
- Define classes for composite and atomic objects so that they implement the same interface

![[composite-pattern.png]]
- `Leaf`s are `Component`s
- `Composite`s are collections of `Component`s, as well as overall being a `Component`

Composite is very effectively combined with strategy

# Template Pattern

>[!Warning] Problem
>How to build generic components that are easy to extend and use without replicating code?

**Solution**
- Define a family of algorithms, encapsulate each one, and make them interchangeable
- Allows the implementation of invariant parts of an algorithm once and leave it to the subclass to implement the behaviour that can vary

A *template* is a method that defines an algorithm as a set of steps. One or more of these steps is defined to be abstract and implemented by a subclass


# Observer Pattern
>[!Warning] Problem
>How to we get updates from an object without constantly polling it?

**Solution**
- Aggregate several listeners in the class of interest, each listener implements a `Listener` interface that exposes a `notify()` or `update()` method.
- Typically we implement the class of interest as an abstract class, which is extended by the concrete class of interest.
