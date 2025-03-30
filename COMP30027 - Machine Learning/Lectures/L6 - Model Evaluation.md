


# Random Holdout
Randomly *partition* data into "training" or "test"
- A portion of the data is "held out"; never seen during training
- Model is only tested on unseen data

**Common Splits** (train-test)
- 50-50
- 80-20
- 90-10
- (N-1)-1 *leave-one-out*

There's a tradeoff between having enough training data and a representative test set.
## Repeated Random Subsampling
Random holdout repeated multiple times:
- Randomly assign data to "training" and "test"
	- Usually with a fixed split
- Train a new model on "training" data
- Test on the "test" data

Final evaluation: average over all iterations


*Slower*, 
# Cross-Validation
How big is $m$? ($m$-fold cross validation)

More folds = fewer test instances / more training instances per partition

**Common choices**
- $m=10$
- $m=5$
Mimics 90-10 or 80-20 holdout, but more reliable

Best choice: *Leave-one-out cross-validation*
- $m=N$ (number of instances)
- Maximises training data
- Far too slow to be used in practice, unless $N$ is tiny

## Practical Issues
Should we ensure the proportion of classes is identical in the training vs. test set?
- Random sampling may produce different proportions
- *Stratification* or *vertical sampling* - training data and test data both have the same distribution as the dataset as a whole

**Inductive Learning Hypothesis:**
Any model which approximates the target function well over a large training set will also generalise to unseen examples

However, machine learners  also suffer from *inductive bias* - assumptions made about the data to build the model and make predictions


## Validation Set
Sometimes data is split into train/validation/test

Validation set is a "test" set for your training data
- Used to choose weights or parameters
- Check if the model converged to a good solution

Why use a validation set?
- Too expensive to train models for all combinations of parameters
- If we choose parameters on the *whole* training set, we can overfit

# Evaluation Metrics

Accuracy is a good start, but we'd like to know more about what the model's doing.

$$\text{Accuracy} = \frac{TP + TN}{N}$$
Consider a 2-class problem where the goal is to find a class of interest ("positive" class) among uninteresting distractors ("negative" class).

From this we get the classification results:
- True positive
- False positive
- True negative
- False negative

**Error rate**:
$$\text{Error Rate} = \frac{ER_0 - ER}{ER_0}$$
Change in error rate relative to a base model's error rate


**Precision**
Disincentivises false positives
$$\text{Precision} = \frac{TP}{TP + FP}$$
>[!cite] Idea
>Out of everything we *claimed* is positive, how many were actually positive?

**Recall**
Disincentivises false negatives
$$\text{Recall} = \frac{TP}{TP + FN}$$
>[!note]
>Also called sensitivity!

**Specificity**
Proportion of true negative cases the model was able to detect
$$\text{Specificity} = \frac{TN}{TN+FP}$$

