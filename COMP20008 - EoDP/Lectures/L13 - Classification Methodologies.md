


## Predictive modelling 

### Classification

We're trying to predict whether a record falls into a category based on a set of information



Given a collection of record (*training set*)

Build a categorical model:
$$y=f(x_1, x_2, ..., x_n)$$
- $y$: *discrete value* - target variable
- $x_1, x_2, ..., x_n$
- $f$ function that maps record to category


*Training set* is used for training the model, which is evaluated on the *test set*.




### Regression


Build a categorical model:
$$y=f(x_1, x_2, ..., x_n)$$
- $y$: *continuous value* - target variable
- $x_1, x_2, ..., x_n$
- $f$ function that maps record to category


>[!note] Regression vs Correlation
> Regression models are predictive, correlation models simply observe trends.


## Techniques


### Decision Trees - Classification

Build a tree-like structure where each internal node represents a condition with a yes/no outcome.

Leaf nodes are the categories.


#### Hunt's Algorithm

Let $D_t$ be the set of training records that reach a node $t$
- If $D_t$ contains records that belong to the class $y_t$, leaf is labelled $y_t$
- If $D_t$ is an empty set, then $t$ is a leaf node labelled as default class $y_d$
- If $D_t$ contains records that belong to more than one class, use an attribute test to split the data into smaller subsets
	- Recursively apply to subsets

Determining the best split:

![[decision-tree-split.png]]


**Node Impurity**

Entropy can be viewed as an *impurity measure*
We want to minimise entropy


>[!tldr] Note
>We want to maximise the *decrease* in entropy from the parent node (before the split) to the child nodes (after the split)

$$Gain = H(Parent) - H(Parent | Child)$$


To compute overall information gain, we subtract the *weighted average* of the child node entropies from the root node's entropy. (They're weighed by the number of records in each node)


We repeat this for all splits that we are considering to find the one that produces the greatest gain of information.




**Splitting Based on Ordinal Attributes**

Multi-way split:
- Use as many partitions as distinct values

Binary split:
- Divides values into 2 subsets (need to find optimal partitioning)

**Splitting Based on Continuous Attributes**

Discretisation

Condition-based splitting