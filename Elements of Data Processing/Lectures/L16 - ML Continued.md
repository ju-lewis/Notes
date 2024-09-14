
## Cross Validation
Changing test-train split partitions (e.g. cycling through all possible 10-90 splits) to get a better understanding of model accuracy


### Repeated Cross Validation
Repeat N-fold validation $r$ times
- For example 5 times

Smooths the effect of random selections


So if we did 10-fold cross validation 5 times, we'd be training and testing the model *50 times!*


## Hyperparameter Selection

Suppose we wish to choose the best $k$ for a k-NN classification model
- Here $k$ is the hyperparameter

We never look at test data
- Leads to overfitting

For hyperparameter selection we further partition the training set into:
- Training subset
- Validation subset

For the values of the hyperparameters we want to test:
We train/fit our model on the *training subset* and record its performance on the *validation subset*
- Then select parameters with the best performance
- Use merged training set to train/fit the final model
- Report final performance using independent test


### Evaluation method - Bootstrap Validation
Relying on smaller samples to draw conclusions

Each smaller sample is drawn randomly from the original dataset with replacement

**Procedure**
1. Draw $b$ bootstrap samples (from training data)
	1. Repeat $b$ times, for each bootstrap sample
		1. Train model on sample
		2. Evaluate performance on its out-of-bag (*OOB*) test/validation data
	2. Report mean and SD of $b$ performance scores


## Classification Metrics

### Confusion Matrix

Breaking down the outcomes of a model into:
- Actual class
- Predicted class

#### Accuracy
$$Accuracy = \frac{\#TP + \#TN}{n}$$
This doesn't really work for rare events

>[!example]
>If 99.9% of people don't have a very specific disease, an extremely accurate model could just be telling everybody that they don't have the disease! (99.9% accuracy)

#### Precision

$$Precision = \frac{\#TP}{\#TP + \#FP}$$

"Out of all positive predictions - how many were true positives?"

Use when you don't want false positives.

#### Recall

$$Recall = \frac{\#TP}{\#TP + \#FN}$$

Use when you don't want false negatives.



These metrics all scale to multi-class classification
- Positive and negative become classes
- e.g. True `A`, False `B`, False `C`, etc.


## Regression Metrics

### Sum of Squared Errors
(Also mean squared error)

$$MSE = \frac{SSE}{n}$$

### Root Mean Squared Error

### Mean Absolute Error
Much less sensitive to outliers

$$MAE = \frac{1}{n}\sum^{n}_{i=0}{y_i - \hat y_i}$$


## Feature Selection 

### Classification
What makes a feature good? - Highly correlated with the class
- Likely to improve performance of a prediction model

**Ranking-based Feature Selection**
- Compute *Mutual information* for each feature and class label
	- How much more do we know about the class when we know $f_i$?


There are potential issues with *univariate feature selection*
- XOR example (can't predict based on 1 feature)