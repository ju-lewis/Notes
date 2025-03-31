# Instances:
![[L2 - Basics of Machine Learning#Terminology]]

Instance-based learning is simply supervised learning with example instances.

## Feature Vectors

A vector locates an instance as a point in an n-dimensional space
- The angle and distance uniquely identify instances


### Similarity and Dissimilarity
**Similarity:**
- Numeric measure of how alike 2 objects are
- Higher when objects are more alike
- Often falls in the range $[0,1]$

*Nominal*: attributes must be exactly the same
*Ordinal*: 
*Interval or Ratio*: $s = -d$

**Dissimilarity:**
- Numeric measure of how unlike 2 objects are
- Often not constrained (can be infinitely dissimilar)

*Nominal*: attributes must be different
*Ordinal*: Absolute value of the difference, divided by the number of values (where mapped to integers $0$ to $n-1$)
*Interval or Ratio*: $d = |p-q|$


### Distance Measures
A distance measure is a function that takes 2 points in space as arguments
- Non-negative
- Obey triangle inequality
- Commutative

>[!note]
>Dissimilarity is not always distance! For example set difference ($A - B$ where $A$, $B$ are sets) is a measure of dissimilarity but does not observe the triangle inequality and is not commutative.

**Examples**:
- Manhattan distance
- Cosine distance
	- Cosine of the angle $\theta$ between vectors $\vec{a}, \vec{b}$
	- Magnitude no longer matters!

#### Nominal Variables
Option 1: Convert categories to numbers
Option 2: One-hot encoding


# Nearest Neighbour Classification

**For any new instance:**
- Find the most similar instance(s) in the training data
- Use them to choose the test label

Typically we take the nearest $k$ neighbours and take the majority label

The closest point: max similarity or min distance

We can also weight the averages for the majority vote based on distance to the participating training instances

## Design Decisions
- Data scaling
- Distance metric
- Tie breaks
- Choosing $k$
- Weighting


### Data Scaling / Normalisation
In real-world datasets, attribute may have very different ranges

>[!example] Predict a home's water usage using a 1-NN classifier:
>**Attributes:**
>- Num. occupants
>- Num. bathrooms
>- House price
>  
>  Here the house price will likely be the only factor that influences the decision as it can be on the order of millions, while the other features are likely $\lt10$


Normalisation ensures all variables have similar ranges and contribute similarly to distance
- Min-max scale to range 0-1
	- $x' = \frac{max(x) - x}{max(x) - min(x)}$
- Standardise to have mean=0 and std=1
	- $x' = \frac{x - mean(x)}{std(x)}$


### Choosing $k$
With a small $k$ we end up with incredibly noisy decision boundary, as only the closest point influences the decision

### Weighting Strategies
**Equal weight**: Simple majority class
**Inverse Linear Distance**: $w_j = \frac{d_{max} - d_j}{d_{max} - d_{min}}$
**Inverse Distance**: $w_j = \frac{1}{d_j + \epsilon}$
- Epsilon is required to ensure we never divide by 0


### Breaking Ties
**Random choice**
**Increase $k$**
**Use a different strategy than a majority vote**
**Take the nearest point**


>[!note] Choosing $k$
>Generally we should set $k$ to an odd value, as you are much more likely to get ties with even values.


### Implementation
A typical implementation involves the brute-force computation of distances between a test instance and every training instance
- Very computationally expensive at test time!

K-NN classifiers are *lazy learners*
- There is no computation done at training time
- No learning is done, it just stores the entire training set
	- Classical machine learning models are generally much smaller than the dataset
- All computation is done at test time when comparing against the training set

## Strengths and Weaknesses
**Strengths:**
- Simple, instance-based, model free
- Can produce flexible decision boundaries
- Incremental

**Weaknesses:**
- Requires a useful distance function
- Arbitrary $k$ value
- Lazy learner
- Prone to noise and the curse of high dimensionality
