

# Part 1

## Q1.1 - Main Success Scenario

**Scenario:** Store manager adding, removing, or updating item in their catalogue.


---
**Scope**: LazyFair - Online shop and delivery system
**Level**: User goal
**Primary Actor**: Store manager
**Preconditions**: A valid account for the store exists
**Supporting Actors**: Inventory management (database) system


SM = store manager

1. SM authenticates on behalf of the store with the app using a login system
2. SM navigates to a catalogue page
3. SM selects desired operation from a menu (add, delete, update)
*Add*:
4. SM enters the name, description, and price of the item
5. SM adds images to the item
6. *SM connects item to inventory management system*
7. SM confirms changes


## Q1.2 - Group Discussion
- Does the scenario make sense?: *Yes*
- Are there any missing steps?: *No*
- Is the level of detail appropriate?: *I don't think so*
- Any other questions you come up with.


## Q1.3 - Alternate Scenarios

*Alternate Scenario 1*: Updating an item
   4a. SM selects an item from the catalogue
1.   SM makes modifications to name, description, price, or images
2.   SM confirms changes

*Alternate Scenario 2*: Deleting an item
   4b. SM selects an item from the catalogue
1.   System prompts SM for confirmation
2.   SM confirms deletion

*Alternate (Failure) Scenario*: Item deletion canceled
4c. SM Selects item from the catalogue
1.   System prompts SM for confirmation
2.   SM cancels deletion

# Part 2

## Q2.1 - Use Case Diagram


![[workshop-use-case-diagram.png]]

## Q2.2 - Show Your Understanding

1. *What are the qualities of a well written use case?*
It is descriptive but not overly technical (clear to a member of the business). There are no missing steps (i.e. it is a complete description) and each step clearly leads to the next.

2. *When designing software, how many use cases should you write? Justify your answer!*
It depends on the complexity and functionality of the software. Use cases and alternate scenarios will inherently arise from decision points in the software/business requirements. In essence, they should cover all of the business requirements but nothing more.

3. *How does use case text differ from a use case diagram? Do we need both?*
The use case text provides a story detailing actors utilising/interacting with the system under discussion. A use case diagram clearly displays the interactions and dependencies within the system. They both provide a different perspective into the software's design.

4. *There are three kinds of actors that can participate in a use case: primary, supporting, and offstage. What are the differences between them? Use an example.*
A primary actor is the main person or system interacting with the system under discussion in a use case (e.g. a customer ordering a pizza using Tony's Pizza system)

A supporting actor provides a service to the system under discussion (e.g. a payment provider in an online shopping system)

An offstage actor is indirectly involved in a use case, as in they are affected by the scenario without interacting with the software. (e.g. Government taxation records for a POS system)

5. *What do you think is the biggest challenge to writing a quality use case?*
Writing with the correct level of detail is difficult, as you must ensure that they entire scenario is sufficiently described without losing meaning or usefulness due to unnecessary verbosity.


