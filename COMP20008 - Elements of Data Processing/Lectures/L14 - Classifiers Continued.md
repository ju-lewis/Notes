

## Nearest Neighbour Classifiers

>[!note] Basic Principle
>If it walks like a duck, quacks like a duck, then it's probably a duck.

Which records in the training set are most similar to the test record?


**3 Required Things**
- The set of stored records
- Distance metric for record comparison
- The value of $k$, the *number of nearest neighbours* to retrieve


**Process**:
1. Compute distance to other training records
2. Identify $k$ nearest neighbours
3. Use class labels of nearest neighbours to determine the class label of unknown record (e.g. through majority vote)

Typically Euclidean distance is the most used distance metric

We can use distance weighting: $w_d = 1/d$

### Choosing $k$

If $k$ is too small - sensitive to noise points
If $k$ is too large, neighbourhood may include points from other classes





