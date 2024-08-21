
## Clustering
Grouping data based on attributes

**Challenges:**
- It's difficult to visualise higher dimensional data
	- We can't visually cluster for $n^{th}$ dimensional data

We need to automatically determine these *clusters*


**Identifying Clusters**
- Must assign each object to only one cluster
- We want similar objects in a cluster, different objects in different clusters.
- We want each cluster to be 'summarised' by its *centroid*

**Standard clustering metrics:**
- Minimise intra-cluster distance
- Maximise inter-cluster distance


We can represent each object/instance as a vector, allowing us to compute distance metrics (e.g. Euclidean)

We ideally want to normalise each attribute into the range $[0,1]$ before computing distance (this prevents a given feature from 'dominating' the position)


### K-Means Clustering

1. First determine the desired number of clusters (e.g. K=5)
2. Randomly pick K cluster centroids
3. For each data point, determine its closest centroid
4. Move each centroid to the mean position of its cluster's data points
5. New centroids => new cluster boundaries
6. Repeat update steps until no further changes.


Typically the initial seed points are assigned randomly
Usually closeness is computed using Euclidean distance

The algorithm only converges to a *local optimum* (different clusters can arise from the same dataset resulting from random seed points)

We can use clusters for outlier detection.

**Disadvantages:**
- Doesn't work well with different sizes and densities
- Doesn't work well with non-circular shapes

#### Finding K - The Elbow Method
What's the best K?

We can compute the "Within Cluster Sum of Squared distance" (WCSS)
$$WCSS(k) = \sum_{c=1}^k\sum_{x_i \in c}||x_i - \bar{x_c}||^2$$

When graphing the WCSS against K, we can find the point where diminishing returns becomes apparent (the 'elbow' of the graph)

### Visual Assessment of Clustering Tendency (VAT)

A (dis)similarity matrix is an adjacency matrix for all of the data points, containing the distances between each pair.

The distances are computed across all features (dimensions).

We can visualise the dissimilarity matrix as a *heat map* 
- Brighter square -> lower distance
- Darker square -> greater distance

We can assess similarity of objects by how similar their colours are (for adjacent objects)

**How do we order the clusters?**




