

Classifier combination is the process of constructing a classifier by aggregating the outputs made by multiple *base classifiers*


## Construct Base Classifiers

### Instance Manipulation
- Generate multiple training datasets through sampling
- Train a base classifier over each (e.g. bagging)

### Feature Manipulation
- Generate multiple training datasets through different feature subsets 
- Train a base classifier over each (e.g. random forest)

### Algorithm Manipulation
- Semi-randomly tweak internal parameters within a given algorithm 
- Generate multiple base classifiers over a given dataset


## Bias and Variance
Analysing the *generalisation error* of a predictive model
From the model's perspective:
- **Bias**: the tendency of a classifier to make systematically wrong predictions
- **Variance**: the tendency of producing different models or predictions for different training sets using the sam learner

Lower bias and variance -> better generalisation


# Combination Methods
## Bagging

**Bagging** = **bootstrap aggregating**

- Intuition: the more data, the better the performance

How can we get more data out of a fixed dataset?
- Construct new datasets through a combination of random sampling and replacement
### Training
Randomly sample the original dataset $N$ times, *with replacement*
- Bootstrap sampling
- We get a new dataset of the same size, where any individual instance is absent with probability $(1-\frac{1}{N})^N$
Construct $k$ random datasets for $k$ base classifiers


### Summary
- Simple method based on sampling (instance manipulation) and voting
- Possible to parallelise computation of individual base classifiers
- Effective over noisy datasets
- Performance is generally much better than the base classifiers

## Random Forest

**Random trees:**
A decision tree, but only some of the possible attributes are considered at each node
- e.g. a fixed proportion $\tau$ of all the attributes
- faster to build than a deterministic decision tree

We combine many random trees to form a random forest.
- Each tree is built using a different Bagged training dataset

**Hyperparameters:**
- Number of trees $B$, which can be tuned based on "out-of-bag" error
- Feature sub-sample size: as it increases, both the strength and correlation increase
	- $\lfloor\log_2|F|+1\rfloor$

**Interpretation**
Logic behind predictions on individual instances can be followed through the various trees


### Summary
- Generally very strong performer, efficient to construct
- Parallelisable
- Robust to overfitting
- Interpretability sacrificed by random selection

## Boosting

>[!Note] Intuition
>Tune base classifiers to focus on the hard-to-classify instances

### Method:

**Summary**:
Iteratively change the distribution and weights of training instances to reflect the performance of the classifier of the previous iteration
- Start with sampling 
- Over $T$ iterations, train a classifier and update the weight of each instance according to whether it was correctly classified
- Combine the classifiers via *weighted voting*


1. Initialise a weight vector with uniform weights
2. Loop:
	1. Apply a weak learner to weighted training samples
	2. Increase weights for misclassified examples
3. Weighted majority voting on trained classifiers

>[!Example] AdaBoost Example
> ![[adaboost-diagram.png]]
### Summary:
- Cannot be parallelised (it's an iterative sampling method)
- Uses weighted voting
- Homogenous classifiers
- Minimise instance bias
- Prone to overfitting


# Stacking
**Level-0**: Base Classifiers
- Given training dataset $(X, y)$
- Train different classifiers: e.g. SVM, Naive bayes, DT
**Level-1**: Classifier Combination
- Construct new attributes based on Level-0 attributes
	- If there are $M$ level-0 classifiers, add $M$ attributes
	- Discard *or* keep original data $X$
	- Consider other data if available (NB probability scores, weights of SVM)
- Train meta-classifier (e.g. logistic regression) to make final prediction

### Summary
- Able to combine heterogenous classifiers with varying performance
- Mathematically simple but computationally expensive method
- Generally, stacking results in as good better results than the base of the best classifiers



