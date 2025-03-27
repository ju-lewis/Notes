
# Evaluation Continued

## Multiclass Evaluation

Confusion matrix
- Compares ground truth against predicted classes

If you have one class of particular interest, you can evaluate *one-vs.-rest*

Usually, you care about all of the classes:
- Go row-by-row and compute accuracy, precision, recall

**Total Accuracy**
- Sum of the main diagonal divided by num. instances

**Other multi-class quantitative evaluation methods**:
Macro-averaging: Calculate P,R per class and take mean
Micro-averaging: Combine all instances into one pool
Weighted averaging: Calculate P,R per class and take a *weighted average*

## Baseline vs. Benchmark

*Baseline*: simple naive method that we would expect a machine learning method to beat.
*Benchmark*: established rival technique to which we are comparing our method

In practice, these definitions are often confused

### Common Baselines:

**Random baseline:** Guess a label uniformly from the available labels
**Zero-R baseline:** Always guess the most common label in the dataset

**Others**:
- Regression: always guess the mean value
- Object Detection: always guess the middle of the image

>[!cite] Test Set Error
>Mean absolute difference between true and predicted label


# Decision Trees

## One-R Baseline
- Consider only one feature (one-rule) to classify the instance

The motivation behind decision trees is to take this one-r baseline, and after making a decision considering if we still have any ambiguity in the prediction, if so we consider another single attribute (otherwise we've already classified the instance!)


## Classifying New Instances

Trace down the decision tree, following the conditions 

## ID3 Decision Tree Construction

Iteratively construct the decision tree

### Entropy

In the context of Decision Trees, we are looking at the class distribution at a node:
- We want to construct our nodes (i.e. our decisions) such that the child branches have the lowest possible entropy

### Information Gain

The expected reduction in entropy caused by knowing the value of an attribute

Compare:
- The entropy before splitting the tree using the attribute's values
- The mean information *after* the split was performed

### Mean Information
Weighted average of the entropy over the children after the split

>[!example] Decision Tree Entropy
>
>We are classifying instances based on the weather 'outlook' (Sunny, Overcast, Rainy)
>
>**Step 1:** Compute the *root* entropy (Entropy of all the instances)
>**Step 2:** Split on 'outlook'
>**Step 3**: Compute the entropy for the instances after the split (sunny, overcast, and rainy instances)
>**Step 4**: Take the weighted average (based on P(sunny), P(overcast), P(rainy)) of the entropies
>**Step 5**: Root entropy - Mean information = Information gain
>


Information gain tends to prefer highly branching attributes

Subsets are more likely to be pure (above a purity threshold) if there is a large number of attribute values.
- May result in overfitting/fragmentation

### Gain Ratio

Gain ratio reduces bias for information gain towards highly-branching attributes by normalising relative to the split info

**Split Info** (SI) is the entropy of a given split (evenness of split)


$$GR(R_A|R)=\frac{IG(R_A|R)}{SI(R_A|R)} = \frac{IG(R_A|R)}{H(R_A)}$$

### Discussion of ID3
- ID3 is an inductive learning algorithm
- ID3 searches a space of hypotheses for one that fits the training examples
- ID3 performs a simple-to-complex hill-climbing search
	- Greedy search with no backtracking

We generally want the smallest tree (Occam's Razor; generalisability)

Prefer the shortest hypothesis that fits the data.
- A short hypothesis that first the data is unlikely to be a coincidence


# Summary
- ID3 Algorithm
- Information gain
- Gain ratio
- Theoretical and practical properties of ID3-style decision trees
