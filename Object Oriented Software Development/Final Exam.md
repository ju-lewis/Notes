### Time allowed: 120 minutes
# Structure
1. 20 MCQ (40 marks)
2. 3 LAQ (80 marks)

Total: 120 Marks


# Content
- Basic Java Concepts
	- Classes/Objects
	- Properties, behaviours
	- Defining classes from specification
	- Getters, setters, construction
	- Instance, static, local
- Software Tools
	- Git
	- Maven
	- IntelliJ Debugger
	- Bagel
	- JUnit5
- Arrays, Strings, IO
	- Arrays
	- Strings
	- Command Line Arguments
	- User Input (Scanner)
	- Files (BufferedReader, FileReader)
	- Standard Ouput
	- File Output (PrintWriter, Filewriter)
- Principles of OOP
	- Inheritence
	- Privacy, Information hiding
	- Shadowing, privacy leaks
	- Overriding
	- Object class
	- upcasting, downcasting
	- polymorphism (sub-type, runtime, parametric)
	- Abstract classes/methods
- Interfaces
	- When to use an interface
	- Inheritance vs interface
	- `Sortable`
- Relationships
	- Textual analysis
	- UML
	- Class Diagrams
- Generics
	- Generic classes
	- Generically typed objects
	- Generically typed methods
- Collections
	- Java collections (List, ArrayList, )
	- Java maps (Hashmap, Hashset)
- Design Patterns
	- What design patterns are
	- Understand specific design patterns
- Exceptions and Error Handling:
	- Understand what exceptions are
	- Handle exceptions
	- Throw vs Throws
- Software design and testing
	- Writing better code
	- Designing better software
	- Testing (JUnit5)
- Event-Driven Programming
	- Describe the even-driven paradigm
	- Describe application
	- JavaFX
	- Implement basic programs
- Advanced Java and OOP
	- Enums
	- Variadic parameters
	- Functional interfaces
	- Lambda expressions
	- Method references
	- Streams


# Revision Workshop
## Generics (Parametrised Polymorphism)

Bounding generic types:
```java
public <T extends Number, E extends Number> int add(T a, T b) {
	return a + b;
}
```

## Exception Handling

## Collections and Maps
Collections: Framework of

## Design Patterns
**Singleton**:
- Creational
- Ensures only 1 instance (globally)
- Contains a static instance to `Singleton`
- Private constructor
- Public `getInstance`
	- Returns instance if not `null`
	- Creates and returns instance if `null`
**Factory Method**:
- Creational
- Delegating creation of classes to an **ABSTRACT** 'factory/Creator' class 
- The abstract creator produces *concrete* creators
- The concrete creators can then create products
**Template Method**:
- Structural
- Contains an *abstract* parent class that implements common steps for solving a problem
- Any datatype-specific steps are abstract, and are implemented by specific subclasses
**Strategy Method**:
- Structural
- Uses a `Strategy` interface, of which several *Concrete Strategies* implement for solving a problem
- The `Context` chooses a strategy with `setStrategy` for solving the problem
- The `Client` contains a context
**Observer Pattern:
- Behavioural
- Subscriber/Observer is an interface
- Publisher/Subject can `subscribe`, `unsubscribe`, and `notifySubscribers`

## Event-Driven Programming
- State - state of an object (e.g. on, off, clicked)
- Event - created when an object's state changes
- Callback/Listener - A method that is triggered when an event occurs

## Streams and Filters:



## Practice Questions:
### Question 1:
You have been tasked with designing the software system for an independent supermarket
store.
The *store* has *3 types of employees* – *cashiers, stockists, and managers*. Each employee
has a *6-digit employee number*, and the system stores their *name*, *address* and *phone
number*. An employee *is able to clock in and clock out of a shift.*
Cashiers are able to *checkout*, which takes a list of items and produces the total cost. A
stockist is able to *stock an aisle*, and is able to check if an aisle needs to be re-stocked. A
manager has a unique password, and is able to approve a refund.
When a new employee is hired, that employee is added to the system.
The store contains multiple aisles. Each aisle has a corresponding aisle number, and
contains multiple items. The system can check the aisle number that a particular item is on.
An aisle can be regular, or a freezer aisle. A freezer aisle stores its ideal temperature and its
current temperature.
Each item has a name, a price and an expiration date.

Part A
```java
public abstract class Employee {
	private String id;
	private String name;
	private String address;
	private String phoneNumber;
	
	public void clockIn();
	public void clockOut();
}

public class Cashier extends Employee {
	public double checkout(Item[] items);
}

public class Stockist extends Employee {
	public void stockAisle(Aisle aisle);
	public boolean checkAisle(Aisle aisle);
}

public class Manager extends Employee {
	private String password;
	
	public void approveRefund();
}

public class Aisle {
	private int number;
	private List<Item> items;
	
	public boolean hasItem();
}

public class FreezerAisle extends Aisle {
	public final double IDEAL_TEMP;
	
	private double currentTemp;
}

public class Item {
	private String name;
	private double price;
	private Date expDate;
}

public class Store {
	private List<Employee> employees;
	private List<Aisle> aisles;
	
	
	public void hireEmployee(Employee employee);
	public int aisleLookup(Item item);
}
```

Part B
Test 1:
- Description: Ensure system handles searching for non-existent items correctly
- Input: An item that is not contained in any of the aisles
- Output: -1
Test 2:
- Description: Ensure an employee cannot clock out without clocking in
- input: Call `clockOut` without having called `clockIn`
- Output: No change of state should occur (no clocking out event recorded)

### Question 2:

Part A
```java
public class File<T> {
	private String filename;
	private T contents;
	
	public <T> File(String filename, T contents) {
		this.filename = filename;
		this.contents = contents;
	}
	
	public void setFilename(String filename) {
		this.filename = filename;
	}
	public String getFilename() {
		return filename;
	}

	public <T> void setContents(T contents) {
		this.contents = contents;
	}
	public <T> T getContents() {
		return contents;
	}
}
```


Part B:
```java
public class Folder {
	private Hashmap<String, File<?>> files;
	
	public void addFile(File input) {
		
		// Check if it already exists
		if(files.get(input.filename)) {
			input.setFilename(input.getFilename + " (1)");
		}
		files.put(input.filename, input);
	}
	
	public <T> void updateFile(String filename, T contents) {
		File newFile = new File<T>(filename, contents);
		
		if(files.get(filename)) {
			files.put(newFile.filename, newFile);
		}
	}
	
	@Override
	public String toString() {
		String out = "FOLDER CONTENTS\n";
		for(String fname : files.keySet()) {
			out += String.format("%-13s: ", fname);
			out += (files.get(fname) + "\n");
		}
		out += String.format("%--13s\n", "-");
		
		return out;
	}
	
}
```


### Question 3:

```java
public abstract class Currency {
	private double price;
	public void setPrice(double price) {
		this.price = price;
	}
	public double getPrice() {
		return price;
	}
}

public class AVAX {
	private static AVAX instance = null;
	
	private AVAX() {
		
	}
	
	public static AVAX getInstance() {
		if(instance == null) {
			instance = new AVAX();
		}
		
		return instance;
	}
}

public class ETH {
	private static ETH instance = null;
	
	private ETH() {
		
	}
	
	public static ETH getInstance() {
		if(instance == null) {
			instance = new ETH();
		}
		
		return instance;
	}
}

public enum TransferType {
	DEPOSIT,
	SEND
}

public class History {
	private TransferType type;
	private Currency c;
	private Double quantity;
	
	public History(Currency c, Double quantity, TransferType type) {
		this.c = c;
		this.quantity = quantity;
		this.type = type;
	}
}

public class Wallet {
	private HashMap<Currency, Double> balances;
	private ArrayList<History> histories;

	public void deposit(Currency c, Double quantity) {
		// Update balance
		Double amount = balances.get(c);
		if(amount == null) {
			amount = 0;
		}
		balances.put(c, amount + quantity)
		// Record operation
		histories.add(new Hisory(c, quantity, DEPOSIT));
	}
	
	public void send(Currency c, Double quantity, Wallet targetWallet) {
		// Check Balance
		Double amount = balances.get(c);
		if(amount == null || amount < quantity) {
			throw new RuntimeException();
		}
		// Decrease Current Balance
		balances.put(c, amount - quantity);
		
		// Increase Target Balence
		targetWallet.deposit(c, quantity);
		
		// Record Operation
		histories.add(new History(c, quantity, SEND))
	}
	
	public void printBalance() {
		for(Currency c : balances.keySet()) {
			System.out.println(c + " " + balances.get(c));
		}
	}
	
	public void printHistory() {
		for(History h : histories) {
			System.out.println(h.type + " " + h.c + " " + h.quantity);
		}
	}
}
```