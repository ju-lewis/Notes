
>[!Note] Main Goal
>Identify good features to reduce redundancy and irrelevant information and improve performance.


# Wrappers

Choose a subset of attributes that give the best performance on the validation set.


**Advantages**
- Can find the subset with optimal performance for the learner
**Disadvantages**
- Not practical, takes a long time to compute

## Practical Wrappers

### Greedy Approach - Forward Selection
1. Train and evaluate model on each single feature
2. Choose the best attribute
3. Repeat until convergence

The termination condition is when accuracy stops improving

Run time is $\frac{m(m-1)}{2} = 1 + 2 + ... + (m-1) + m$
- In practice, convergence occurs much faster

**Disadvantages**
- Can converge to sub-optimal solutions
- Assumes independence of attributes

### Ablation Approach - Sequential Backward Selection
1. Train and evaluate a model with all attributes
2. Remove each attribute, train and evaluate model
3. Choose the attribute that causes the least performance degradation
4. Repeat until *divergence*
	1. Accuracy drops below a threshold $\epsilon$

**Advantages**
- Removes most irrelevant attributes at the start
- Performs best when the optimal subset is large
**Disadvantages**
- Running time: cycles can be slower with more attributes
- Not feasible on large datasets


# Embedding Methods
Models perform features selection as part of the algorithm

>[!Example]
>- Decision trees
>- Regression model with regularisation
>	- e.g. Linear regression with L1-norm regulariser (LASSO)


Still benefit from other feature selection approaches!


# Filtering Methods
Most popular strategy
- Evaluate "goodness" of each attribute

Consider each attribute separately: linear time in number of attributes

We typically look for *high correlation* (or inverse correlation) with the interesting class

## Point-wise Mutual Information (PMI)
Let $A$ be the set of attributes and $C$ be the set of class labels
- $a$ is a single attribute
- $c$ is a single class label
$$PMI(A=a,C=c)=\log_2\frac{P(a,c)}{P(a)P(c)}$$

## Mutual Information (MI)
Consider the PMIs of all the combinations of $a, \bar{a}, c, \bar{c}$

$$MI(A,C)=\sum_{i\in\{a,\bar{a}\}}\sum_{j\in\{c,\bar{c}\}}P(i,j)\log_2{\frac{P(i,j)}{P(i)P(j)}}$$ 
### Contingency Tables
Compact representation of the frequency counts


![[contingency-table.png]]
We can then compute $P(a,c), P(a), P(c)$, etc. from the table.
$$P(a,c)=\frac{\sigma(a,c)}{M}$$

## $\chi^2$ (Chi-squared)

Similar idea with MI, but different solution
- Conduct statistical test to check the independence of an attribute and the class

$$\chi^2=\sum_{i\in\{a,\bar{a}\}}\sum_{j\in\{c,\bar{c}\}}\frac{(O_{i,j}-E_{i_j})^2}{E_{i,j}}$$


## Types of Attributes

### Nominal Attributes
What do we do if the nominal attribute has multiple values (not just a binary Y/N)?

**Strategy 1:**
Treat the attribute as multiple binary attributes
- Split into several features
	- e.g. Weather = {Sunny, Rainy, Overcast} -> Sunny = {Y, N}, Rainy = {Y, N}, Overcast = {Y,N}

**Strategy 2:**
Expand formulae and contingency table

Our formulae now have to iterate across more attribute values, not just Y/N

### Continuous Attributes

**Strategy 1:**
Estimate probabilities by fitting a distribution

**Strategy 2:**
Discretise values (binning)

