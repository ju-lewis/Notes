
# Naive Bayes Summary

Naive Bayes can significantly struggle with features that are *heavily* dependent
- Orientation *and* shape example


Why does naive Bayes usually work, despite the wrong assumption of conditional independence?
- We don't need a perfect estimate of $P(c|T)$ for every class


**Strengths**
- Simple to build, fast
- Computations scale well (dimensionally)
- Explainable
- Works with various data types, just need to change how you compute $P(x_i|c_j)$ for each attribute
**Weaknesses**
- Inaccurate when there are many missing $P(x_i|c_j)$ values
- Conditional independence assumption becomes problematic for complex systems


# Discrete and Continuous Data

Naive Bayes (in the form previously discussed) assumed nominal data, so we can't just use continuous values
## Continuous Data

We can't just plug in the numbers directly to our naive Bayes classifier as they'll only be given individual training points from a continuous (infinite) set.
- We can perform *binning* to fix this (see [[L5 - Probabilistic Learning Continued#Data Conversion|Data Conversion]] below)

# Data Conversion

## Nominal -> Numeric

We can perform a *one-hot encoding* of the data
- Best way to represent nominal values in a continuous space, but increases dimensionality of the space


## Numeric -> Nominal

### Discretisation

**Binning Strategies**
Equal width vs. Equal frequency vs. Naturally looking at breaks in the data

Equal Width:
- Sensitive to outliers

Equal Frequency:
- Equal frequency usually works better for more skewed data (requires sorting values)
- Sensitive to sampling bias

Natural Grouping:
- Use some clustering method (e.g. k-means) to find natural clusters

>[!example] Natural Grouping Example
>![[COMP30027 - Machine Learning/imgs/binning.png]]

### Supervised Discretisation

Group values into class-contiguous intervals
- Sort values, and identify breakpoints in class membership
- We want each bin to be 'as pure as possible', as it results in the strongest predictor of the label

>[!warning]
>Very likely to overfit training data, and results in a huge number of classes


# Gaussian Naive Bayes

A popular pdf to pick for continuous data is the *Gaussian/normal distribution* 
We can derive the parameters $\mu$ and $\sigma$ from the training data

Because the labels are inherently categorical, we can predict direct probability masses, conditioning on continuous variables.

>[!example]
>![[gaussian-naive-bayes.png]]
>
>We can just look at the parameters to see when it'll classify into specific categories
>
>We can also look at the error of the model.


# Multinomial Naive Bayes

Works for data with *counts*.

Probability of getting outcomes $X_1, ..., X_k$ with counts $x_1,...,x_k$ ($\sum_ix_i=n$) probability of each outcome is $p_1,...,p_k$




