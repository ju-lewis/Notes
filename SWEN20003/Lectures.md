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
		double area = Math.PI * radius * radius;
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


