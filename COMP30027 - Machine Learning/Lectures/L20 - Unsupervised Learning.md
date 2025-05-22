
>[!Info] Embeddings
>An **embedding** of an input is the network's response to the input at some layer

# Clustering
- No explicit or implicit definition of class
- Learn structure from data alone
- Typically we introduce our own assumptions

**Deterministic vs. Probabilistic**
- Deterministic = each instance is a member of one cluster (no overlap)
- Probabilistic = each instance has a *weight* in each class (clusters overlap)

Why choose one over the other?:
- Deterministic when we need hard boundaries (exact decisions)


## K-Means Clustering
Start with $k$ random centroid points
- Update centroids based on mean position of captured points

### "Soft" K-Means Clustering
Probabilistic variant of K-Means

**Solution**: apply softmax function to the distances to each centroid
- Note, the output values are not technically probabilities, they just have the properties of a probability distribution

## Finite Mixtures
A **finite mixture** is a distribution composed of $k$ component distributions
- Used to represent subgroups of latent factors in a dataset

**Gaussian Mixture Model** (GMM) represents a distribution composed of $k$ Gaussian distributions

>[!Info] Expectation Maximisation
>Parameter estimation method with guranteed positive hill-climbing characteristics relative to gradient of log-likelihood
>
>Used to estimate hidden parameters

### GMM with EM Algorithm
- Basic idea: generalisation of k-means


Expectation step
- Likelihood instance is from a given distribution
Maximisation step
- Updating distribution parameters using log likelihood
- Compute weighted mean and std for each distribution
- Mixing parameter = mean($\hat \gamma$)

**EM Log Likelihood**
- Sum the logs of $\sum_j P(c_j)P(x_i | c_j))$

If the change in log likelihood drops below a threshold, we consider the model to be converged

>[!Example]
>For data modelled by a mixture of two Gaussian distributions, we weight the sum of two normal distributions (weighting forms the parameters)


We don't know which distribution produced each instance, but given some parameters (e.g. $\gamma, \mu_1, \sigma_1, \mu_2, \sigma_2$) we could estimate how likely each distribution was to have generated each instance


#### Advantages:
- Guaranteed "positive" hill climbing behaviour
- Fast to converge
- Results in probabilistic cluster assignment
#### Disadvantages:
- Has an element of randomness (outcome is somewhat probabilistic)
- Can get stuck in local maxima
- Need to assume number of clusters


## Kernel Density Estimation (KDE)

Suppose you have some data points x1,x2,...xn. How do we represent the probability distribution form which the data originated?

Option 1: Discretise into $k$ bins
Option 2: Model it as a Gaussian distribution
Option 3: Model is as $k$ Gaussian distributions
Option 4: KDE

KDE is kind of a combination of all of the above

We create a Gaussian distribution for each of the data points, then we sum them all up to form the KDE
- The standard deviation of the Gaussian kernel sets the *bandwidth*, which determines how jagged/smooth the KDE is

**Advantages**:
- Model arbitrary distributions
- No assumptions about shape of distribution
**Disadvantages**:
- Need to choose a kernel bandwidth
- Need many parameters


# Unsupervised Evaluation

>[!Info]
>We use unsupervised learning for down-projection, identifying clustering, generate new samples from the modelled distribution, etc.

There are no "ground truth" labels, how can we tell if a model is correct?
- Subjective evaluation
- Check similarity of clusters over multiple iterations
- Cross validation
- Supervised evaluation (if labels become available at some point)


We can optimise KDE using *KDE Naive Bayes*

**High Cluster Correlation**
- Instances in a given cluster should be close
**High Cluster Separation**
- Clusters should be far apart
**Cluster Compactness**
- Compute the sum of square errors
- Euclidean for numeric
- Hamming for nominal


If labels are available, evaluate the degree to which class labels are consistent within a cluster and different across clusters
- Purity
- Entropy
