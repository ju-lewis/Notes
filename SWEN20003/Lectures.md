# Week 1
## Data Abstraction
**The technique of creating new data types that are well suited to an application by creating new classes.**

A class is a special kind of programmer-defined data type


# Week 2

## Encapsulation
**The ability to group data (attributes) and methods that manipulate the data to a single entity through defining a class.**

***Instance Variables*** are unique to each instance of the class (shown in the example below)

- Classes are characterised by encapsulation

```java
// Defining a class

public class Circle {
	public double centreX;
	public double centreY;
	public double radius;
	
	public double computeArea() {
		double area = Math.PI g* radius * radius;
		return area;
	}
}
```


By creating the `Circle` class, you have created a new data type `Circle` - **Data Abstraction**

## Instantiating Classes
The declarations:
```java
Circle aCircle;
Circle bCircle;
```

Create null-references to `Circle`s - no memory is allocated.

Objects are *null* until they are *instantiated*

```java
Circle aCircle = new Circle();
```

## Getters and Setters
Generally Initialising/updating/accessing instance variables is done by defining specific methods.

These are known as **Accessor/Mutator** methods, or informally as **Getter/Setter** methods.

Getters and setters are usually used to allow information hiding, visibility control, and privacy. *Consider scenarios like input sanitisation.*

## Constructors
A constructor is a method that is run when the object is instantiated.

Constructors *must* have the same name as the class.

```java
public class Circle() {
	public double radius, x, y;
	// Constructor
	public Circle(double newRadius, double newX, double newY) {
		radius = newRadius;
		x = newX;
		y = newY;
	}
}
```

## Method Overloading
- Method overloading is when multiple methods have the same name, but are distinguished by their signature
	- Number of arguments
	- Type of arguments
	- Position of arguments
- Any method can be overloaded
- Method overloading is a type of *polymorphism* (same method - different behaviour)
- **Not to be confused with *Method Overriding***

### Polymorphism is the ability to process objects differently based on their type.

Method overloading is a form of compile-time polymorphism

What if the *variable names in the constructor* share the same names as the *instance variables?*

The `this` keyword can be used to specify that the variables refer to the current object instance.

For example:
```java
public class Circle() {
	public double radius, x, y;
	// Constructor
	public Circle(double radius, double x, double y) {
		this.radius = radius;
		this.x = x;
		this.y = y;
	}
}
```

This allows the compiler to differentiate between the instance variables and constructor arguments (local variables).

## Defining Static Variables
Static variables are shared between objects (only one copy - as they share a singular reference to memory): e.g. count of the number of objects of the type that have been created.

If we wanted to count the number of `Circle`s that we instantiate, we could add  
```java
public static int numCircles = 0; 
```
to the class definition of `Circle`.

We could then increment it whenever the `Circle` constructor method is called.

To access static variables we do:
```java
Circle.numCircles;
```

***Note: we access the variable from the class directly, not from an object instance as it's shared.***

## Static Methods
Static methods are also called directly from the class

## Static Summary:

**Static Members:** Methods and attributes that are not specific to any object of the class.
**Static Variable:** A variable that is shared among all objects of the class; a single instance is shared among all objects of the class.
**Static Method:** A method that does not access or modify any instance variables of the class.

# Week 3
## Standard Methods

Some useful standard methods:
- `equals()`
- `toString()`
	- Called by `System.out.println()` by default
- `copy()`
	- Performs a deep copy of an object
	- Takes the form of a constructor

### copy() method:

```java
public class Circle {
	public double x, y, radius;
	public Circle (double x, double y, double radius) {
		this.x = x;
		this.y = y;
		this.radius = radius;
	}
	
	public Circle (Circle aCircle) {
		// This is now a copy method
		if (aCircle == null) {
			System.exit(0);
		}
		this.x = aCircle.x;
		this.y = aCircle.y;
		this.radius = aCircle.radius;
	}
}

// Example call:
Circle c1 = new Circle(0.0, 0.0, 1.0);
// Now copy the data of c1 into c2
Circle c2 = new Circle(c1);
```


## Packages in Java

A **package** is a group of classes and interfaces in a bundle, that can then be handled together using an accepted naming convention.

Works similar to libraries in C; can be developed, packaged, imported and used by other Java programs/classes

It is another level of *encapsulation*.

### Creating Packages
```java
package <directory_name>;
```

### The Default Package
All the classes in the current directory belong to an unnamed package called the `default` package - no package statement is needed.

As long as the current directory is part of the CLASSPATH variable, all the classes in the current default package are automatically available to the program.


## Information Hiding
The ability to hide the details of a class from the 'outside world'.

### Visibility Modifiers:
- Public
	- Method/attribute is visible everywhere
- Private
	- Only visible within the class, not visible within subclasses or package
- Protected
	- Only visible within class / subclasses / package

The default is visible within the class AND package.

### Mutability
- **Mutable:** A class that contains a public mutator method, any instances are called mutable object
- **Immutable:** A class that contains no methods (other than constructors) that can change any of the instance variables

## Delegation through Association
A class can delegate its responsibilities to other classes
An object can invoke methods in other objects through *containership*
This is an *Association* relationship between the classes

For example, for the `Circle` class, we could *delegate* the coordinates to another class:
```java
public class Point {
	private double x, y;
	
	public Point(double x, double y) {
		this.x = x;
		this.y = y;
	}

	public double getX() {
		return this.x;
	}
	public double getY() {
		return this.y;
	}
}
```

Now the `Circle`'s position is defined by a `Point` instead of 2 separate doubles.


## Wrapper Classes

Wrapper classes provide *utility methods* to handle the corresponding primitive type.

| Primitive | Wrapper Class |
| --------- | ------------- |
| boolean   | Boolean       |
| char      | Character     |
| int       | Integer       |
| float     | Float         |
| double    | Double        |
|           |               |

## Automatic Boxing/Unboxing

- **Boxing** is converting a primitive to its corresponding wrapper class
- **Unboxing** is getting the primitive value from a wrapper class


## Software Tools 

### Version Control with Git
![[Git.PNG]]

### Unimelb GitLab Server:
https://swen20003.eng.unimelb./edu.au/

#### We are using *Maven* for build management

### IntelliJ Debugger



## Bagel Framework

A simple bagel program is as follows:

```java
import bagel.*;

public class BagelTest extends AbstractGame {
	// Define entry point
	public static void main(String[] args) {
		BagelTest game = new BagelTest();
		game.run();
	}
}
```


**The update method:**

```java
@Override
public void update(Input input) {
	// Your code goes here
}
```


# Week 4

## Arrays
- **A sequence of elements of the *same* type arranged in order in memory**

### Declaring arrays:
```java
int arr1[] = {0,1,2,3};

int arr2[] = new int[4];
```

Multi-Dimensional Arrays
```java
int[][] nums = new int[10][10];


// Initialising:
for(int i = 0; i<nums.length; i++) {
	nums[i] = new int[/*length of subarray*/];
}
```

Arrays can also be used to store references to objects

Indexing beyond the length of the array throws an *out-of-bounds error*.

### Array methods:
Indexing
- `a1[i];`
Length
- `a1.length;`
Equality:
- `Arrays.equals(a1, a2);`
Sorting:
- `Arrays.sort(a1);`
Printing:
- `System.out.println(a1.toString());`

Java supports `for-each` loops:
```java
for(/*Variable Type*/ element : array) {

}
```

### Resizing Arrays:
As array size is constant, resizing requires creating a new array:
```java
int[] a1 = new int[4];
// We now want to store 6 more integers
a1 = new int[a1.length + 6];
```

## Strings

#### Java strings behave similarly to Python strings, except double quotes *must* be used

Appending strings can be done with `+` and `+=`. Like Python, classes like strings in Java have custom implementations of the addition operator, so using `+` to append to a string implicitly converts the types of any non-string operands.

### Some useful String methods:
```java
String str = "Hello, world!";

// .split() tokenises the string by a given delimiter
System.out.println(str.split(" ").toString());

// Case conversions
System.out.prinln(str.toUpperCase());
System.out.prinln(str.toLowerCase());

// Substring searching
str.contains("Hell"); // Boolean indicating prescence
str.indexOf("lo"); // Substring location
str.substring(2,7); // String slicing

// Modifying
str.replace("world", "there");
```

As strings are actually objects (i.e. a reference to a location in the Heap), we can't use standard equality comparison and are required to use:
`str1.equals(str2)`
For equality checks.


## Input and Output

### Command Line Arguments
`args` is an array of strings containing the command line arguments passed to the Java program

***NOTE:*** `args[0]` points to the first argument *after* the program name.

#### Command Line Arguments in IntelliJ
Because IDEs like IntelliJ do a lot behind the scenes before running the program, command line arguments are input slightly differently.

In IntelliJ you have to set the "run configuration" to pass CLI flags


### Input Using Scanner:

To use the `Scanner` class in a program:
```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
```

#### ONLY EVER CREATE 1 SCANNER PER PROGRAM!

Useful Scanner methods:
`.nextLine()` Reads until a newline is received (as a String)
**Alternatively you can use:**
`.nextBoolean()` For Boolean values
`.nextInt()` For Integers
and
`.nextDouble()` for Doubles
`.next()` Reads any characters up to a delimiter (whitespace)

Note that the scanner does *not* automatically downcast types (e.g. float to int).
Make sure your input matches what is expected by the code!

Also note:
`.nextLine()` is the **only** method that consumes a newline character from the input, so it may need to be used following other `.nextXXX()` methods


We can use `.hasNext()` to check if there is *any* input to be read, or `.hasNextXXX()` to check if we can read tokens of type `XXX` 


### Reading Files:
We can import the file reader classes:
```java
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.IOException;

public class ReadFile1 {
	// Example program that reads every line from 'test.txt' and prints it
	public static void main(String args[]) {
		try (BufferedReader br = 
			new BufferedReader(new FileReader("test.txt"))) {
			
			String line = null;
			while((text = br.readLine()) != null) {
				System.out.println(line);
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

`FileReader()` is a 'low level' file reader for simple character reading
`BufferedReader` is a higher-level wrapper that permits reading Strings

These should be used in `try/catch` statements



#### We can also use Scanner to read files
However, `Scanner` has a smaller internal buffer and is slower than `BufferReader`.

Example program that counts the number of main headings in an HTML file:
```java
public class HeadingParser {
	public static void main(String args[]) {
		if(args.length < 2) {
			System.out.println("File name not provided.");
			return;
		}
		int headingLines = 0;
		
		try (BufferedReader br = 
			new BufferedReader(new FileReader(arg[0]))) {
			String line = null;
			while((text = br.readLine()) != null) {
				// Check if an <h1> tag is present in the line
				if(line.contains("<h1>")) {
					headingLines++;
				}
			}
			System.out.println("Number of lines with headings: " + headingLines);
		} catch (Exception e) {
			e.printStackTrace();
		}	
	}
}
```

### Writing To Files:
We can do something similar to write to files with the imports:
`java.io.FileWriter;`
`java.io.PrintWriter;`

The writer is created in the same manner as the BufferReader:
```java
PrintWriter pw = new PrintWriter(new FileWriter("text.txt"));
```

We can then use the methods:
`pw.println()` and `pw.format()`

Note that the .format() method prints to the file as well as formatting the String!


# Week 5

## Inheritance
A form of abstraction that generalises behaviours to parent classes, allowing child classes to *inherit* the behaviour.

**Superclass:** The parent or base class.
**Subclass:** The child or derived class

Define common attributes and methods in the Superclass
Subclass automatically contains all (public/protected) instance variables and methods in the superclass.

Subclasses should be 'more specific' versions of the superclass


### Example (Chess):
We can define a 'Piece' superclass that contains common information like position, isAlive, etc.

We can *extend* this piece definition to each kind of piece as a subclass, provided specific functionality and information unique to that piece.

This allows us to avoid rewriting basic functions like getters and setters for common information.

#### Inheritance Example:
```java
public class InherinanceTester {
	public static void main(String args[]) {
		// This trivially works, a Rook is a Rook
		Rook rook1 = new Rook();
		
		// This works as a Rook "is a" Piece
		Piece rook2 = new Rook();
		
		// This DOESN'T WORK!!! A Piece "is not a" Rook
		Rook rook3 = new Piece();
	}
}
```

### Initializing with Constructors

We DON'T copy and paste parents constructors into subclass constructors.

The keyword `super` can be used to invoke (call) the constructor of the super class.

```java

public class Piece {  
	
	// Here we define common behaviour across ALL pieces
	
	private int currentRow;  
	private int currentColumn;  
	
	public Piece(int currentRow, int currentColumn) {  
		this.currentRow = currentRow;  
		this.currentColumn = currentColumn;  
	}  
	
	public int getCurrentRow() {..}  
	public void setCurrentRow(int currentRow) {..}  
	public int getCurrentColumn() {..}  
	public void setCurrentColumn(int currentColumn) {..}  
}

public class Rook extends Piece {
	
	// Here we provide Rook-specific implementations
	
	public Rook(int currentRow, int currentColumn) {
		// We can call the Piece constructor with super
		super(currentRowm, currentColumn);
	}
	
	public void move(int toRow, int toColumn) {..}
	public boolean isValidMove(int toRow, int toColumn) {..}
}
 ```

The `super` keyword must be the first statement in the subclass constructor if it's used.


### Inheriting and Overriding Methods

Consider the methods: `move` and `isValidMove`

With the `isValidMove()` method, all pieces must have this behaviour, with the same signature.

Additionally, some of the behaviour across pieces for check move validity is common, e.g. checking the move is within the board bounds (not outside)


#### Overriding Methods

When a method is defined only in the parent class (and has the correct visibility), it gets called *regardless* of the type of object created.

When a method is defined with the *same signature* in both the parent and child classes, the method that executes depends entirely on the *type of object* as opposed to the type of reference. (e.g. `isValidMove()` method)

In the second case, the child class **overrides** the method in the parent class.

Annotating `@Override` can indicate that the method is overriding a method in the parent class.

### Extension Through Overriding

If we know there is common behaviour between the parent and child classes, we can move the common logic to the parent class (to avoid needlessly rewriting)

In this case, we can use the `super` keyword to call the parent class (superclass) method.

```java
public class Rook extends Piece {
	public boolean isValidMove(int toRow, int toColumn) {
		if(!super.isValidMove(toRow, toColumn)) {
			// Generic move validity checks failed
			return false;
		}
		
		// Now we can do Rook-specific move validation
	}
	
}
```


#### NOTE: Overriding CANNOT change return type, unless changing to a *subclass* of the original.



### Pitfall: Method Overriding
`private` methods cannot be overridden as they can't "see" the private method


### Restricting Inheritance
The `final` keyword can be used to prevent overriding of a method/attribute

For example, with Chess pieces, we don't want child classes to override the parent's `move` method, as all pieces simply move to the target coordinates, so we can use the `final` keyword to prevent it from being overridden


### Privacy Leaks
Defining attributes as `protected` allows updating them directly from child classes.

However, this should be avoided because it results in *privacy leaks*. The attributes of the parent classes should be access via `public` or `protected` methods in the parent class.

### Access Control
Methods in the parent class that are only used by subclasses should be defined as `protected`


### Shadowing
Shadowing occurs when a child class has the same attribute names (instance variables) as the parent class.


### Object Class

All classes implicitly inherit from the `Object` class

`toString()`
`equals()`

To override the `equals` method:

```java
@Override
public boolean equals(Object o) {
	if (this == o) return true;
	if (o == null) return false;
	if (getClass() != o.getClass()) return false
	
	// Now we can safely downcast and compared attributes, etc.
	Piece piece = (Piece) o;
}
```

Note that the argument signature must only take a base `Object` class object for overriding to occur.

## Polymorphism

### Overloading
Ad-hoc polymorphism
### Overriding

### Substitution

### Generics




### Abstract Classes
A class that represents common attributes and methods for objects, but *cannot* be instantiated.

An abstract class is an *incomplete* class.

#### Abstract Methods:
The `abstract` keyword defines a superclass method that is common to *all* subclasses but has not implementation. Each subclass provides their own implementation through overriding.

Back to the Chess example, we could have:
```java
public abstract boolean isValidMove(int toRow, int toColumn);
```


# Week 6

## Interfaces

Interfaces are *vague, distant* relatives of abstract class:
- Defines an abstract entity - can't be instantiated
- Can only contain constants and abstract methods
- Defines behaviours/actions that are common across a number of classes

All interfaces represent a *"Can do"* relationship.

They provide a behavioural contract for objects.


Interface names are generally called `<...>able` and relate to an action.

For example, objects with the `Driveable` interface have a callable `drive()` method.


### Defining Interfaces

```java
public interface Printable {
	int MAXIMUM_PIXEL_DENSITY = 1000;
	
	void print();
}
```

Like when a class `extends` an abstract class, a class can `implement` an interface:

```java
public class Image implements Printable {
	
	void print() {
		// We need to implement EVERY method in the interface
	}
	
}
```


### Default Methods

Classes can be "forced" to have an implementation of a method, that can then be overridden.

```java
public interface Printable {
	default void print() {
		System.out.println(this.toString());
	}
}
```


### Why use interfaces?

Even though `Clothing` and `Seatbelt` can both be "worn", there is no logical relationship between them; they should not be represented through inheritance! 


**Implementing a `makeNoise` method**:

A `Dog` *is an* animal, a `Cat` *is an* animal, so it makes sense to use an abstract class with a `makeNoise()` method.

A `Dog` *can* make a noise, a `Vehicle` *can* make a noise, but it doesn't make sense to use inheritance as they're not related at all (what would we even call the superclass???) - so we use an `interface`

## Sorting

Java sorts using:
```java
Array.sort(obj);
```

But how does Java sort or compare any items? **Using interfaces.**

### Comparable Interface:
A class that implements `Comparable<ClassName>`
- Can be compared with objects of the same class
- Must implement `public int compareTo(<className> obj)`

#### compareTo
- Defines a method allowing us to *order* objects
- Compares *exactly 2* objects, A and B
- Returns a negative integer, zero, or positive integer if object `A` (this) is <, \==, > than object `B`

### Next Level Abstraction
Classes can only inherit from 1 class, but can implement multiple interfaces.

### Subtype Polymorphism
```java
// Inheritance
Robot robot = new WingedRobot();

// Interfaces

```


# Week 7

## Software Design

### Design Algorithm

1. Identify Classes *Noun extraction*
2. Identify Class Relationships *Identify has-a, is-a, can-do*
3. Refine Classes and Relationships
4. Develop a Class Diagram *Combine classes and relationships*
5. Represent using an accepted notation *UML is a widely accepted industry standard*

### UML
A graphical modelling language that can be used to represent object oriented analysis, design, and implementation


#### Representing a Class in UML
![[UML Example.png]]


**Note**: attributes can have a default value:
Example: `xPos: int = 0`

Function arguments must be named:
Example: `render(name: String): void`


**Privacy Constraints** are represented as follows:
- \+ Public
- \~ Package-private (default)
- \# Protected
- \- Private

**Multiplicity** is represented as:
- Finite e.g. \[10]
- Range (Known) \[1..10]
- Range (Unknown) \[1..\*]
- Range (Zero or More) \[\*] 

**Static** methods/attributes are <span style="text-decoration: underline">underlined</span>



### Representing Class Relationships

#### Association
- Represents a *has-a* relationship between objects
- Allows objects to *delegate* tasks to other objects
- Shown by a solid line between classes

When a class is *contained* by another, we always use an association, never write the nested class inside of the outer class.

Properties of association
- Name
- Role labels
- Directionality
- Multiplicity
![[UML-association.png]]
![[UML-association-2.png]]

**Association Type: *Aggregation***
Where one class "has" another class, but both exist independently
e.g. A pond can have ducks

Represented by a 'diamond' on the connecting line on the side of the containing class.

There can also be *compositional association*

Represented by a closed diamond on the side of the owner.
#### Generalization (Inheritance)


#### Realization (Interfaces)

Combined realization and generalization

![[UML-realization.png]]
#### Dependency

Dependency represents weak relationships between classes

Represented by a dotted arrow

### UML Drawing Tools
- draw.io
- LucidChart - student email
- StarUML

# Week 8
## Generics

Generics enable generic logic to be written that applies to any class type.

### Comparable Interface

The `Comparable` interface:
```java
public interface Comparable<T> {
	public int compareTo(T other);
}
```

`T` is a *type parameter* or type variable.

When `T` is given a value (type), every instance of the *placeholder* variable is replaced.

The value of `T` is literally a type (class/interface)

Whoever is implementing the interface must specify the type


***Comparing WITHOUT Generics***
- Our comparison function takes an `Object o`
- We need to check if `o instanceof T` (if not return -2)

### ArrayList

`ArrayList<T> arr = new ArrayList<T>();`

Features of ArrayLists:
- Can be iterated (for-each)
- Automatically handles resizing

Limitations:
- Doesn't shrink automatically (can consume more memory than required)
	- We can invoke `trimToSize()` to free the required memory
- Can't store primitive data types


### Defining a Generic Class
A generic class is a class defined with an arbitrary type for a field, parameter or return type.

- The type parameter is included in angular brackets after the class name in the class definition heading
- A type parameter can have any reference type
- We usually use `T`, `S`, `B` as the parameter names

Example:
```java
public class Sample<T> {
	private T data;
	
	public void setData(T data) {
		this.data = data;
	}
	
	public T getData() {
		return data;
	}
}

Sample<Integer> 
```


### Bounded Type Parameters

```java
public class Generic<T extends <class, interface>> {
}
```

Example:

```java
public class Generic<T extends <Robot, Comparable>> {
}
```


### Generic Methods
```java
public <T> T genericMethod(T arg);
```


```java
public <T> int CountOccurrences(T[] array, T item) {
	int count = 0;
	
	if(item == null) {
		for(T arrayItem : array) {
			count = arrayItem == item ? count + 1 : count;
		}
	} else {
		for(T arrayItem : array) {
			count = arrayItem.equals(item) ? count + 1 : count;
		}
	}
	return count;
}
```

## Collections and Maps

### Collections:
A framework that permits storing, accessing and manipulating lists (an ordered collection)


#### Sorting with ArrayLists

We can create a class that handles the sorting for us, by implementing the `Comparator` interface:

```java
class RatingComparator implements Comparator<Movie> {
	@Override
	public int compare(Movie m1, Movie m2) {
		if (m1.getRating() < m2.getRating()) return -1;
		if (m1.getRating() > m2.getRating()) return 1;
		else return 0;
	}
}
```

Note that this is not the same as the `compareTo` method in the `Comparable` interface

Usage example:
```java
ArrayList<Movie> movies = new ArrayList<Movie>;
// Assume movies is initialized here

// This implementation requires the comparison to be in the movie class
Collections.sort(movies);

// This implementation allows separate comparisons to be used
Collections.sort(movies, new RatingComparator());

// Another example of using an external comparator
Collections.sort(movies, new NameComparator());
```

We can implement these `Comparator` classes as *Anonymous Inner Classes* (note: this works very similarly to anonymous functions in other languages)

```java
Collections.sort(movies, new Comparator<Move>(){
	@Override
	public int compare(Movie m1, Movie m2){
		if (m1.getRating() < m2.getRating()) return -1;
		if (m1.getRating() > m2.getRating()) return 1;
		else return 0;
	}
})
```



### Maps:
A framework that permit storing, accessing and manipulating key-value pairs.


#### TreeMap
Elements are automatically sorted (Binary tree) - Requires `Comparable` implementation

#### HashMap

Generic class that takes two types: `K` (the key) and `V` (the value)

```java
HashMap<String, Book> library = new HashMap<String, Book>();

Book b1 = new Book("Example Author", "Example Title", 100);

library.put(b1.author, b1); // We have now stored the book by its author

for(String author : library.keySet()) {
	Book b = library.get(author);
}
```


***We are we using generics here?***

The only alternatives would be:
- Defining everything as `Object` (would need massive if-else chains to determine classes - not maintainable)
- Rewrite your code for any types you may use it with

# Week 9

## Design Patterns

Design patterns systematically document re-occurring design solutions so that they can be reused.

Good designers reuse solutions - they do not design everything from scratch.
### Introduction and Motivation

*Intent* The goal of the pattern
*Intent*
*Applicability*
*Structure* Graphical representations of the pattern, likely UML
*Participants* Involved classes/objects
*Consequences* A description of results and side effects
*Implementation* Example of 'solving a problem' with the pattern
*Known uses*

### Singleton Pattern
A pattern that enforces having only a single instance and provides a global point of access to it.

*Motivation*: There are cases where only one instance of a class must be enforced with easy access to the object.

- Private constructor
- Public static `Singleton getInstance()` method
	- This method determines if the instance is null
	- If it is null, creates the instance
	- Otherwise just return the instance

*Known Uses*: `CacheManager`, `PrinterSpooler`
### Factory Method Pattern
***Problem:*** Creating objects in the class that require (uses) the object is inflexible

*Factory*: A general technique for manufacturing (creating) objects
*Product* An abstract class that generalises the objects being created by the factory (e.g. different types of gameEngine)
*Creator*: An abstract class that generalises the objects that will consume/produce products

![[Factory-pattern.png]]

Note that the `factoryMethod()` is `abstract`, this delegates object creation to subclasses.
*Encapsulates* objects by allowing subclasses to determine what they need

*Intent*: To generalize object creation
*Applicability*: When sister classes depend on (and create) similar objects
*Consequences*: Object creation in the superclass is now decoupled from the specific object required.
### Template Method Pattern
Building generic components that can be *extended*, *adapted*, and *re-used* is key to good design.

***Templating uses inheritance***

We want to be able to write an algorithm once, and re-use it for other datatypes. To achieve this, we create a generic version of the algorithm and create classes that implement if for specific data-types.
![[Template Pattern.png]]
#### Example - Insertion-sort:
```java
public abstract class AbstractInsertionSorter {
	private static int operations = 0;
	protected int length = 0;
	
	protected abstract int doSort() {
		for(int i=0; i<length; i++) {
			for(int j=i; j>0; j--) {
				if(outOfOrder(j-1)) {
					swap(j-1); // Swaps with `j`
				}
			}
		}
		return operations;
	}
	protected abstract boolean outOfOrder(int index);
	protected abstract void swap(int index);
}

public class IntInsertionSorter extends InsertionSorter {
	
	// We define the array in this class!!
	private int[] A = null;
	
	public int sort(int[] A) {
		this.A = A;
		length = A.length();
		return doSort();
	}
	
	@Override
	protected abstract boolean outOfOrder(int index) {
		return A[index] > A[index+1];
	}
	
	@Override
	protected abstract void swap(int index) {
		int temp = A[index];
		A[index] = A[index+1];
		A[index+1] = temp;
	}
}
```

There are still issues with this, for example if we want to implement the `InsertionSorter` for `Double`s, we'll need to copy much of the logic over.
### Strategy Pattern
Completely separates the algorithm from the datatypes, resulting in very versatile algorithms.

***Strategy pattern uses delegation***

```java
public class InsertionSorterS {
	static int operations = 0;
	private int length = 0;
	private SortHandle itsSortHandle = null;
	
	public InsertionSorterS(SortHandle handle) {
		itsSortHandle = handle;
	}

	public int sort(Object A) {
		itsSortHandle.setArray(array);
		length = itsSortHandle.length();
		operations = 0;
		
		if(length <= 1) return operations;
		
		for(int i=0; i<length; i++) {
			for(int j=i; j > 0; j--) {
				if (itsSortHandle.outOfOrder(j-1)) {
					itsSortHandle.swap(j-1);
				}
				operations++;
			}
		}
		return operations;
	}
}
```

Here we have delegated the comparison and swapping to a `SortHandle`.

```java
public interface SortHandle {
	public void swap(int index);
	public boolean outOfOrder(int index);
	public int length();
	public void setArray(Object array);
}
```

![[Strategy-Pattern.png]]

### Observer Pattern
When a part of the code is 'watching' (observing) an event

The observer pattern decouples the subject and observers using a publish-subscribe style communication pattern. (The observer no longer has to watch everything the subject does)

Observers can be watching multiple subjects, e.g. students (observers) watching both the lecturer and the screen (subjects).

When the subject changes, it will publish a notification that the observers can read and analyse to decide if they need to react to it.

#### Subject:
An "important" object, whose state (or change in state) determines the actions in other classes
#### Observer:
An object that monitors the subject in order to respond to its change in state

![[Observer-Pattern.png]]

`notifyObservers()` if effectively a `for` loop that iterates through all of the observers and calls `notify()`

This pattern is similar to interrupts (as opposed to polling).


Note that Java has an `Observer` and `Observable` interface in the standard library.

![[Java-Observer.png]]
### Pattern Types

These patterns are based on the *Gang of Four* book, which describes 23 common design patterns.


#### Classes of Problems
- *Creational* - Solutions related to object creation, e.g. Singleton, Factory method
- *Structural* - Solutions dealing with the structure of classes and their relationships: e.g. Adapter, Bridge
- *Behavioural* - Solutions dealing with the interaction among classes, e.g. Strategy, Template Method, Observer

# Week 10
## Exceptions

Exceptions =/= bad, they're just unusual circumstances (particularly in Java/OOP)

Exceptions are classes in Java

### Errors/Mistakes

*Syntax Errors:*
You have written something that isn't legal Java code, so there is a compilation error.

*Semantic Errors:*
Code runs to completion, but results are incorrect. (logic is wrong)
Identified through software testing

*Runtime Errors:*
An error that causes your program to crash; identified through execution.


**Recovering From a Runtime Error Example:**

```java
double divide(double n1, double n2) {
	return n1 / n2;
}
```

This code will crash given an input of `n2 = 0`

Solution 1 - *Do Nothing*:
- Obviously not ideal

Solution 2 - *Guarding / Input validation* (Defensive programming):
- Preventing erroneous inputs based on code context
- Example: ensuring `n2 != 0`
- It is good to both do this in conjunction with proper handling
- Can be difficult to predict all possible erroneous inputs

Solution 3 - *Using exceptions to handle error states*:
- Using `try catch` statements
- We want to be as specific as possible with the exception type caught, especially if error messages are printed
- Java supports `finally` blocks, it is useful to close files in the `finally` block - in general, perform clean up
- Java also supports `catch` chaining (ensure the order is correct)
	- If a superclass comes first in a catch chain, a compile error will occur
- DO NOT CATCH `EXCEPTION`!!

Keywords:
`throw`: respond to an error state by creating an Exception object
`throws`: Indicates a method has the potential to create an exception


`throws`  is used when we don't want to handle the error inside a method directly, as it may need to be handled by the user class


### Defining Exceptions:

All exceptions have 2 constructors

```java
import java.lang.Exception;

public class InvalidRadiusException extends Exception {
	public InvalidRadiusException() {
		super("Radius is not valid");
	}
	
	public InvalidRadiusException(double radius) {
		super("Radius ["+radius+"] is not valid");
	}
}
```

Using the new exception:
```java
public class Circle {
	private double x, y;
	private double r;
	
	public Circle(double x, double y, double r) throws InvalidRadiusException {
		if(r <= 0) {
			throw new InvalidRadiusException(radius);
		}
		this.x = x;
		this.y = y;
		this.r = r;
	}
}
```


### Exception Types:

*Unchecked*: Can be safely ignored by the programmer; most inbuild Java exceptions are unchecked

*Checked*: Must be explicitly handled - will result in a compilation error otherwise

Both Exceptions (Checked) and Errors (Unchecked) inherit from *Throwable*

### Try With

Example:
```java
public void processFile(String filename) {
	try(BufferedReader reader = ...) {
		...
	} catch (FileNotFoundException e) {
		e.printStackTrace();
	} catch (IOException e) {
		e.printStackTrace();
	}
}
```


## Software Design and Testing

### Good Programming Practices

Don't have the datatype in the variable name.

#### Comment Style
- Intended primarily for yourself
- Code should be *self-documenting*; readable without extra documentation
- If your code were removed, comments should be sufficient to "piece together" the algorithm
- Comments should be attached to *blocks* of code

#### Javadoc
- Compiled to HTML
- Used to document packages, classes, methods, and attributes
- Uses '@' tags
- Intended primarily for developers using your program

- Needed for public classes, attributes, and methods
- INCLUDING GETTERS, SETTERS, AND CONSTRUCTORS!


Consider the extensibility of your solutions (fixing/changing/updating).

### Design Principles:

So far we have seen:
- OOP good practice (encapsulation, information hiding, delegation, inheritance, realization, polymorphism)
- Modelling classes and relationships
- Design patterns

#### Modularity:
Decomposing the problem to units (modules) that are easy to understand, manage, and re-use.
- In OOP classes are the basic modules

#### Cohesion
Modules MUST be design to solve clear, focused problems. 
- Classes must be defined to have high cohesion
Example:
- A car with a GPS should not have the GPS functionality defined inside the car class. The car class should be focused only on handling car related things.

#### Coupling
The degree of interaction between modules must be reduced as much as possible.
Designs should have **low** coupling.
- Deciding when to have an association relationship should be done carefully
- Interfaces promote low coupling
- Decide when it is appropriate to pass objects as parameters (dependency) to reduce coupling.

#### Open-Closed Principle
Modules should be **open** to extension, but **closed** to modification.
- In practice, if we want additional/modified functionality, we should extend the base class, not directly modify it.

#### Abstraction
Solving problems by creating abstract data types to represent problem components.

#### Encapsulation
The details of a class should be kept *hidden* or *private*, and a user's ability to access the hidden details should be restricted. Known as **Information Hiding**.

#### Polymorphism
The ability to use an object or method in many different ways; achieved in Java through *ad hoc* (overloading), *subtype* (overriding, substitution), and *parametric* (generics).

#### Delegation
Keeping classes focused by passing work to other classes. Computations should be performed in the class with the *greatest amount of relevant information*


### Poor Design Symptoms
- *Rigidity:* difficulty of modification, because of cascading changes
- *Fragility:* Changing one part of the system causes unrelated parts to break
- *Immobility:* Can't decompose systems into modules
- *Viscosity:* Writing "hacks" to get around problems
- *Complexity:* Premature optimization, etc.
- *Repetition:* Repeated code
- *Opacity:* Difficult to read code


### Bug Fixing
- Print statements
- Google
- Forums

### Software Testing
- Unit Testing - Testing individual units/components independently
- Integrations and System Testing - Integrating units to form the system
- Acceptance Testing - User experience testing


**Unit**: A small, well-defined component with a small number of responsibilities
**Unit Test**: Verifying the operation of a *unit* by testing a single *use case* (input/output), intending for it to FAIL.
**Unit Testing**: Identifying bugs by running a suite of unit tests on all units.


#### Manual Testing
Generally used for reaching difficult edge cases. Not scalable for large projects.
#### Automated Testing
Testing code with automated, purpose built software. Generally faster and more reliable.


### JUnit Automated Testing
In this class we use JUnit5

```java
import org.junit.Test;
```

`assert` a true or false statement indicates the success or failure of a test case.
`TestCase` is a *class* dedicated to testing a single unit. Naming convention is to use append `Test` to the tested classes' name (e.g. `BoardTest`)


`assertArrayEquals(expected, actual)`
`assertTrue(condition)`
`assertFalse(condition)`
`assertEquals(expected, actual)`
`assertNotEquals(expected, actual)`

The overriding of the assertion methods works like this:
- 2 parameters: `expected, actual`
- 3 parameters: `expected, actual, delta`
	- Delta is the maximum non-negative difference (margin of error)

# Week 11

#### JUnit Tags
`@Test`: Marks a method as a test
`@BeforeEach`: Marks a method to be executed before each test method in the class
`@AfterEach`: Marks a method to be executed after each test method in the class
`@BeforeAll`: Runs once before all tests in the classes
`@AfterAll`: Runs once after all of the tests

``
Unit test Example:
```java
public class BoardTest {
	private Board board;
	@BeforeEach
	public void setup() {
		board = new Board();
	}
	
	@Test
	public void testBoard() {
		//Board board = new Board();
		Move move = new Move(0,0);
		assertEquals(board.cellIsEmpty(move), true);
	}
	@Test
	public void testValidMove() {
		//Board board = new Board();
		Move move = new Move(0,0);
		assertEquals(board.isValidMove(move), true);
	}
	@Test
	public void testMakeMove() {
		//Board board = new Board();
		Player player = new humanPlayer();
		Move move = new Move(0,0);
		board.makeMove(player, move);
		assertEquals(board.getBoard()[move.row][move.col], "R");
	}
}
```


Remember to test all edge cases / circumstances, for example when testing if a move is valid, check if it's out of bounds on all 4 board sides.


#### Expected Knowledge:
- Documentation
- Software Design
	- Keyword, definitions, general principles
- Software Testing
	- Keywords, implementing JUnit5 unit tests

#### JUnit Advantages
- Easy to set up
- Scalable
- Repeatable
- Not human intensive
- Incredibly powerful
- Finds bugs

## Event Driven Programming

**Sequential Programming**: A program that is run (more or less) top to bottom
**Event-Driven Programming**: Using *events* and *callbacks* to control the flow of a program's execution based on changes to the program state.
**State**: The properties defining an object
**Event**: Created when the state of something is altered
**Callback/Listener**: A method triggered by an event

Event-driven programming is fundamentally asynchronous


An event is *fired*
An *event handler* is a method in the *listener* that specifies what will happen when the event occurs.

The program no longer determines the order in which things can happen, instead - the events determine the order.

### JavaFX

### Software Development Frameworks
- Normally consists of a set of abstract classes and interfaces
- The partially complete classes can be customized to meet application needs

# Week 12

## Advanced  Java and OOP Concepts

### Enumerated Types
`enums` are collections of constants (all public static)

We can combine `enums` to apply restrictions:

```java
public enum Suit {
	SPADES(Colour.BLACK),
	CLUBS(Colour.BLACK),
	DIAMONDS(Colour.RED),
	HEARTS(Colour.RED);
	
	private Colour colour;
	
	private Suit(Colour colour) {
		this.colour colour;
	}
}
```
In this case, `Suit` is now tied to `Colour`

Default sorting behaviour is the order they're defined in the enum

### Variadic Parameters

Variadic parameters are implicitly converted into an array (treat them as such)

```java
public String concatenate(String... strings) {
	String s = "";
	for(String str : strings) {
		s += str;
	}
	
	return s;
}
```


### Functional Interfaces and Lambda Expressions

A functional interface contains only a single abstract method; also called a Single Abstract Method Interface

```java
@FunctionalInterface
public interface Attackable {
	public void attack();
}
```

Functional interfaces define a clear contract with a single abstract method.

1. Callback mechanism
2. Strategy patterns: implement various strategies that can be easily swapped
3. Stream API: Utilize functional interfaces like 'Predicate', 'Function', and 'Consumer' to manipulate collections



#### Example:
```java
public interface Predicate<T>
```
The `Predicate` functional interface represents a predicate - a function that accepts one argument and returns `true` or `false`.
- Executes the `boolean Test(T t)` method on a single object
- Can be combined with other predicates using the `and`, `or`, and `negate` methods

```java
public interface UnaryOperator<T>
```
The `UnaryOperator` functional interface:
- Represents a function that takes one argument and returns an object of the same type
- Executes the `T apply(T t)` method on a single object

#### Lambda Functions:
A `Lambda Expression` is a technique that treats code as *data* that can be used as an "object" (instantiating an interface without implementing it)

```java
Predicate<Integer> p = i -> i>0;
```


Unary Operator Example:
```java
import java.util.function.UnaryOperator;

public class UnaryOperatorDemo {
	public static void main(String[] args) {
		UnaryOperator<Integer> u1 = i -> i + 1;
		UnaryOperator<Integer> u2 = i -> i - 1;
		
		System.out.println(u1.apply(Integer(10)));
		System.out.println(u2.apply(Integer(10)));
	}
}
```


Consider the method in the `List<T>` class:
```java
public abstract class List<T> {
	public void replaceAll(UnaryOperator<T> operator);
}
```

### Method References

A *method reference* is an object that stores a *method*; can take the place of a lambda expression **IF** that lambda expression is only used to call a single method

```java
UnaryOperator<String> u3 = String::toUpperCase;
```

#### Examples:
```java
/* ---------- STATIC METHODS -------------- */
Class::staticMethod
Person::printWarning

/* ---------- INSTANCE METHODS -------------- */
Class::instanceMethod || object::instanceMethod
String::startsWith || person::toString

/* ---------- CONSTRUCTOR -------------- */
Class::new
String::new

```

```java
public class MethodReferenceDemo {
	public static void main(String[] args) {
		List<Integer> l = Arrays.asList(12,4,5,8,1,56,4);
		Predicate<Integer< p = i -> Number.isOdd(i);
		
		// Comparing lambda function predicate vs method reference
		System.out.println(findNumbers(l, p));
		System.out.println(findNumber(l, Number::isOdd));
	}
	
	public static List<Integer> findNumbers(List<Integer> list, 
		Predicate<Integer> p) {
		
		List<Integer> l = new ArrayList<>();
		for(Integer i : list) {
			if(p.test(i)) {
				l.add(i);
			}
		}
		return l;
	}
}
```


### Java Streams

A stream is an Iterable sequence of data.

#### Example:
```java
list = list.stream()
			.filter(s -> s.length() > 5)
			.filter(s -> s.startsWith("C"))
			.map(String::toUpperCase)
			.collect(Collectors.toList());
```

#### Standard Stream Operations
`map` - converts an input to an output (applies a function to all elements)
`filter` - selects all elements that match a predicate
`limit` - perform a maximum number of iterations
`collect` - collects all stream elements into a collection
`reduce`  - Aggregate a stream into a single value


# Subject Review