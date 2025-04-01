# Pre-Workshop

**Communication Diagrams**
- Like system sequence diagrams, but laid out in 2D space instead of a sequence of line transactions
- The motive is that system sequence diagrams take up a significant amount of space.


Ideally we want:
- Low coupling
	- Limit interfaces between classes
- High cohesion
	- Ensure classes have a clearly definable purpose/responsibilities



# Exercise One - Determining Experts

**1.1** Who should determine the highest bidder in an auction?
- `Listing` tracks a list of 0 or more `Bid`s from participating `User`s, hence it would make send for the `Listing` to have a method for determining the highest bidding `User`


**1.2** Who is responsible for finding all the items within a subcategory?
- `SubCategory` contains all of the items attributed to that subcategory, hence it should be responsible for computing the number of contained items

**1.3** Who is responsible for retrieving past transactions for a user?
- `User` is the only class that is associated with all transactions from a given user. I.e. it 'knows of' all transactions from itself.

# Exercise Two - Handling Creation

**1a** Who is responsible for instantiating transactions?
- `Listing` records all pricing information (through aggregating `Bid`s)
- `Listing` tracks the auction end date, so it know when to create the transaction
- `Listing` can notify `User` through selecting the highest bid

**1b**. Who is responsible for creating bids?
- `User` tracks the listings they are participating in, however since `Listing` aggregates the `Bid`s for itself, it would make sense that the `User` calls a function on a `Listing` to create a `Bid`
- Hence `Listing` is responsible for instantiation

# Exercise Three - Coupling and Cohesion

Coupling is quite high due to the lack of implementation considerations when directly translating between domain and design diagrams. For example, in the creation and storing of transactions, you end up with high coupling between `User`, `Listing`, and `Transaction`.

This could be solved by applying *pure fabrication* to create an adapter between classes such as transaction and user - creating a conceptual interface for transaction instantiation.

# Exercise Four - Controllers

We could have a single facade controller that receives inputs and coordinates

