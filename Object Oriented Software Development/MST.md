# Content:
**Lectures 1-12 (inclusive)**


# Weeks: 
## 1 - Data Abstraction
A class is a programmer-defined type

## 2 - Encapsulation and Classes

- Encapsulation
	- Grouping data and functions to manipulate data within a single entity

- Instantiating Objects
	- `Object obj;` creates a null-reference to an Object (hasn't been instantiated yet)
	- `new Object();`  instantiates the object
	- Constructors *CANNOT* be overriden
- Usually we want instance variables to be private to promote information hiding (provide a public getter/setter interface for accessing and updating data)

- Overloading is creating multiple methods with the same name but different argument signatures - it's a form of compile-time polymorphism
	- Constructors can be overloaded

- Static variables are shared across all objects of the class.
- Static methods are shared across all objects of the class.
	- They cannot update or access instance variables
	- They're called from the class name, not an individual object
## 3 - Packages, Information Tiding, and Software Tools
- Remember the standard methods: `equals()`, `toString()`, `copy()`
- A Package is a group of classes and interfaces in a bundle
	- This is another level of encapsulation
- Visibility modifiers:
	- Public
	- Private
	- Protected
		- Only visible within the class / subclasses
## 4 - Arrays, Strings, and IO
## 5 - Inheritance and Polymorphism

Upcasting (casting from subclass to superclass)
Downcasting (casting from superclass to subclass)
## 6 - Interfaces
