
How do we interpret models?
- **Error Analysis** (Why has a given model misclassified an instance in a certain way?)
- **Model Interpretability** (Why has a model classified an instance in a certain way?)


# Error Analysis


## Basic Approach

**Identifying** different "classes" of errors the system makes (predicted vs. actual labels)

**Hypothesising** as to what has caused the different errors, and testing those hypotheses against the actual data

**Quantifying** whether it is a question of data quantity/sparsity or something more fundamental

**Feeding** those hypotheses back into feature/model engineering to see if the model can be improved




Starting point: a confusion matrix & a random subsample of misclassified instances (non-diagonal counts)

A good starting assumption is that a given "cell" in the confusion matrix forms a single error class
- Target (non-diagonal) cells with very counts


# Parameters

## Hyperparameters vs. Parameters

**Hyperparameters** are chosen by the programmer
**Parameters** are learned by the model (fit to the data)


### KNN Classifier
**Hyperparameters**:
- Value of $K$
- Distance metric
- Weighting strategy
  
 **Parameters**:
- None, the model is "lazy" and just memorizes the whole training set

**Interpretation:**
- Relative to the training instances that give rise to a classification and their distribution in feature space



### Nearest Prototype Classifier
**Hyperparameters**:
- Distance metric
- Feature Weighting
  
**Parameters**:
- Average position of a class in feature space
	- Prototype for each class
	  
**Interpretation**:
- Relative to the distribution of the prototypes in the space, and distance to each prototype


### Naive Bayes
**Hyperparameters**:
- Smoothing Method
- Optionally the choice of distribution used to model the features (e.g. Gaussian for continuous attributes)

**Parameters**:
- Class priors and conditional probability for each feature-value-class combination
- Size: $O(|C| + |C||FV|)$
	- $C$ = set of classes, $FV$ = feature value pairs

**Interpretation**
- Usually based on the most *positively-weighted* features associated with a given instance

### Decision Trees
**Hyperparameters**:
- Attribute selection method (e.g. information gain, gain ratio)
- Stopping criterion
- Maximum depth
**Parameters**:
- Decision tree itself
- Typical size: $O(|FV|)$
	- $FV =$ set of feature-value pairs
**Interpretation**:
- Based on the path through the decision tree

### SVM
**Hyperparameters**
- Penalty term $C$ for soft-margin SVM
- Choice of kernel and any associated hyperparameters
- How to deal with multi-class problem
**Parameters**
- Hyperplane: normal vector + intercept/bias
- Size: $O(|C||F|)$
	- Assuming one-vs-all SVM
**Interpretation**
- The absolute value of the weight associated with each non-zero feature in a given instance provides an indication of its relative importance in classification


# Visualisation and Dimensionality Reduction

Data visualisation is useful for understanding shape and presence of anomalies


## Principal Component Analysis

Central idea: The principal components are 
- linear combinations of the original features
- Orthogonal to each other
- Capture the maximum amount of variation in the data

PCA is generally performed using an eigenvalue solver (e.g. singular value decomposition)


## Confidence
Model's internal score for how well an item fits a class, often expressed as a probability

Confidence score is not "the probability of the model being correct" although it may be correlated

Defined differently for different models
- SVM - distance from classification boundary
- Naive Bayes - Posterior probabilities
- K-NN - (Inverse ?) Distance to the nearest instance of that class

# Summary
- What is error analysis and how is it carried out?
- What are hyperparameters and parameters?
- For each of the primary machine learning algorithms what are the (hyper)parameters and how do we interpret the mode?
- How to use dimensionality reduction and PCA