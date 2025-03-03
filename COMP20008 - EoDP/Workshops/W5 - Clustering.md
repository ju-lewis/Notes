
>[!note] What is clustering?
Finding natural groupings within the dataset

## K-Means Clustering

We can use *K-Means* clustering to produce the clusters - described by their centroids.
- We need to choose the number of clusters before running the analysis
- K-Means doesn't work for more complex shaped data


### How can we find an appropriate number of clusters?

#### VAT

#### Elbow Method




## Hierarchical Clustering

### Agglomerative Clustering

>[!example] Algorithm
>```
>M <- ProximityMatrix(Dataset)
>
>while NumClusters > 1 do
>	NewClusters <- CombineClosestClusters(M)
>	M <- UpdateMatrix(NewClusters, DistanceMetric)
>```

The distance metric can be:
- single-linkage *(Smallest possible inter-cluster distance)*
- full-linkage *(Largest possible inter-cluster distance)*
- average-linkage *(Mean inter-cluster distance)*


