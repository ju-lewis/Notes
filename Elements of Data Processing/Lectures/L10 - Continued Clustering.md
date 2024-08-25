

## Hierarchical Clustering

Produces a set of nested clusters organized as a hierarchical tree.

Visualised as a *dendrogram*
	Tree-like diagram that records the sequence of merges (y-axis is distance)



### Agglomerative Clustering
Start with points as individual clusters, combine until only 1 cluster

**Determining Cluster Distance**
- Min (*single linkage = SLINK*)
	- Gives long 'sausage' clusters
	- Disadvantage: sensitive to noise and outliers (we can 'bridge' our way over)
- Max (*complete linkage = CLINK*)
	- Gives round ball clusters
	- Disadvantage: sensitive to cluster size
- Mean

Process:
1. Create a proximity matrix
2. Let each point be a cluster
3. Merge 2 closest points

For determining the distance between the closest clusters, we use the previously chosen distance metric (min/max/mean)

Remember, we always link the 2 closest points.


### Divisive
Start with 1 cluster, break it down until all points are in their own cluster.


Once a decision has been made to combine 2 clusters, it cannot be undone!
- An object in the wrong cluster will always stay there



## Dimensionality Reduction - PCA

A data analysis algorithm may become confused if paying attention to 'all the points'

**The curse of dimensionality**
- Data analysis techniques that perform well at lower dimensions often perform poorly when dimensionality increases.



**Dimensionality Reduction**
- You want to ignore some irrelevant features
- Select 'most useful' features



**Bag of Words Example**
Given input texts about *summer*

- Group words (with strengths +/-) into categories:
	- Activities: swimming, going to beach...
	- Food: ice cream, watermelon...
	- Clothing: t-shirt, sandals, swimwear...


The dimensions are:
- Orthonormal
- Sorted by strength

The dimensions may not make sense to us!


### Transforming N to n\<\<N dimensions
Transformation should preserve characteristics
If close together before transformation, should be close together after the transformation


### Principal Components Analysis (PCA)
Also known as Singular Value Decomposition (SVD) or Latent Semantic Analysis (LSA)


Find a new set of features that are a linear (weighted) combination of existing features.


**Process**
1. Perform standardisation
2. Calculate covariance matrix of dataset
3. Compute eigenvectors and eigenvalues of covariance matrix.
	1. Eigenvectors => principle components
	2. Eigenvalues => significance of PCs
4. Select the number of PCs to generate feature vectors
5. Apply transformation to standardised dataset


**Limitations**
- Not clear how many dimensions to consider
- Information loss
- Non-intuitive features
- Only linear combinations


