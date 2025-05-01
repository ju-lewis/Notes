

1. Start with a dataset of instances comprised of attributes and labels
2. Build a classifier using a learner and the dataset
3. Assess the effectiveness of the classifier
	- Comparing the predictions with the actual labels on *unseen* data
	- Metrics: accuracy, precision, recall, F1 score, etc.
	

>[!Note] Inductive Learning Hypothesis
>Any hypothesis found to approximate the target function well over a sufficiently large training data set will also approximate the target function well over held-out test examples

**Tensions in Classification**

**Generalisation**
- How well does the classifier apply what it's learned to new data?
**Consistency**
- Is the classifier able to flawlessly predict the class of all training instances?
**Overfitting**
- Has the classifier memorised the training data?

# Overfitting

## Learning Curves
A learning curve is a plot of learning performance over experience or time

For machine learning models, we can plot:
- **y-axis**: performance measured by some metric
- **x-axis**: Training iterations, test-train split, etc.
- **Training learning curve**: performance metric on the training set 
- **Test learning curve**: performance metric on the test set

We can graph both curves together (training and test)
- We want to optimise both
- We also want to minimise the gap between the 2
- Overfitting occurs when the test performance drops but the training performance continues to improve

## Reasons for Overfitting

**Decision boundary distorted by noise**
- Classifier may 'learn the noise' to improve performance

**Limited training set**
- Could be due to a small number of examples
- Could be due to non-randomness in the training examples (sampling bias)


### Solution: Regularisation

In **soft-margin SVM**, the slack variables provide regularisation
- Allow misclassified instances in the training set


In **linear regression**, the norm of the parameters can be used as the regulariser
- Mathematically, a norm is a total length of a vector
- $\|\vec\beta\|_{\mathcal{P}} = \text{Euclidean distance if } \mathcal{P}=2 \text{ Manhattan distance if } \mathcal{P=1}$

We then update the optimisation objective function to account for *regularisation*:
$$\hat \beta = \arg_{\beta} \min[\text{Error}(\vec{\beta}; \{X,Y\}) + \lambda \psi(\vec \beta)]$$

Linear regression with *L2-norm regularisation* (Ridge regression)
- Adding the sum of their squared values to the error term
- Encourages solutions where most parameters are small

Linear regression with *L1-norm regularisation* (LASSO)
- Adding the sum of their absolute values to the term
- Encourages solutions where few parameters are non-zero

## Bias and Variance

In machine learning, bias refers to a number of things:
- **Model bias**
	- Tendency for our model to make systematically wrong predictions
	- Example: in regression, we can determine bias with mean *signed* error
- **Evaluation bias**
	- The tendency for our evaluation strategy to over or under-estimate model performance
- **Sampling bias**
	- If our training or evaluation dataset isn't representative of the population
	- Breaks inductive learning hypothesis


### Evaluation Bias
$Bias(\hat \theta, \theta) = E[\hat \theta(x) - \theta(x)]$

How do we control bias and variance in evaluation?
- Holdout partition size
	- More training data: less model variance, more evaluation variance
	- Less training data but more test data: more model variance, less evaluation variance

Repeated random subsampling and K-fold cross-validation
- Less variance than holdout

Stratification:
- Less model and evaluation bias
