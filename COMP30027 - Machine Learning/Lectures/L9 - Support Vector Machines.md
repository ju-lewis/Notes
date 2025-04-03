

# Nearest Prototype Classification

A parametric variant of nearest-neighbour classification

Calculate the *centroids of each class*, and classify each test instance according to the class of the centroid it's nearest to

>[!note]
>The centroid is calculated simply by averaging the numeric values along each axis for a class

## Drawbacks
- Fails with non-linearly separable classes


# Support Vector Machines
**Goal:** find a straight line/hyperplane that separates two classes

With a linear classifier we're looking for data that's *linearly separable*

## SVM Hyperplanes

A separating hyperplane in $D$ dimensions can be defined by a *normal* $\vec{w}$ and an *intercept* $b$

Assuming our notation uses *column vectors*:
$$\vec{w}^T\vec{x} + b = 0$$

A linear classifier takes the form $f(\vec{x}) = \vec{w}^T\vec{x} + b$
- In 2D space this is a line
- In 3D space it's a plane
- etc.


Consider the distance from a data point to the boundary (hyperplane)
- The confidence of a prediction can be thought of as proportional to distance to the boundary


### Optimal Solution
Aim: find a decision boundary that allows to make all *correct* and *confident* predictions for a given training set

SVM finds an optimal solution:
- Maximises distance between the boundary and the difficult points close to the boundary
- Most stable under perturbations of the inputs

## Margins
Margins are $2\times$ the minimum distance between the boundary and data points
- The *support vectors* are the closest data points to the boundary that define the margin

>[!info] Margin definition
>![[svm-margin.png]]
## Classification using SVM

**Task**: Associate one class as positive (+1) and one as negative (-1)

**Build the model**: Find the best hyperplane $\vec{w}, b$ which maximises the margin between the positive and negative training instances

**How to learn $\vec{w}, b$?**
*Naive (iterative) approach:*
1. Pick a plane $\vec{w}, b$
2. Find the worst classified example
3. Move the plane to classification of the worst example
4. Repeat until the algorithm converges

*Actual method:*
- sets up an optimisation problem to find the separating hyperplane

### Classifying a New Instance
- Find the sign of $f(\vec{t})=\vec{w}^T\vec{t}+b$
- The value of $f(\vec{t})$ can be transformed into a probability, which shows the confidence
- Sometimes we can assign "?" to instances *within* the margin.

SVM has a huge memory advantage over KNN classifiers, as hyperplanes are defined by a very small subset of training instances close to the margin



## Non-linearly Separable

### Soft Margins
Possible large margin solution is better even though one constraint is violated
Soft margins: trade-off between the margin and the number of mistakes on the training data


### Non-linear SVM
Make non-linearly separable problem separable by mapping data into a better representation space
- *Kernel trick*

>[!example]
>Consider using the distance from the origin to the data points as a new dimension value
>
>![[non-linear-svm.png]]
>Concentric circles become linearly separable using this kernel
>- Radial basis function

## Multi-class SVM
Most common approaches for multi-class problems is to convert to a two-class problem:

**One-versus-all**: One classifier to separate one class from the rest of the classes, choose the class which classifies test data point with greatest margin

**One-versus-one**: One classifier per *pair of classes*, choose the class selected by most classifiers
- Computationally expensive because we have $n\choose2$ classifiers


# SVM Summary
- SVM is a linear hyperplane-based classifier for 2-class classification
- SVM selects the hyperplane with *maximum margin*
- *Soft margins* allow some data points to violate the separating hyperplane
- Non-linear SVM transforms data to a new feature space and finds a hyperplane separating two classes in the new space



