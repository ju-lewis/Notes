

# Concept Learning

People can grasp a "class" concept from very limited data
- One (or few) examples
- Noisy features
- Diverse data set
- Ambiguity about feature importance

# Why Probabilistic Models?
- Framework for modelling systems that are noisy/uncertain
- Rules that let you generalise from limited observations
- Based on laws of probability, so gives you an optimal prediction given the available data
	- And the assumptions built into the model


# Probabilistic Learner
Goal is *classification*

We need to build a probabilistic model of the training data, and then use that to predict the class of the test data

In probabilistic terms, given an instance $T$, which class $c$ is most likely?

$$\hat c = \arg \max _{c \in C} P(c|T)$$


Requires a massive amount of data
We need to have seen every possible *combination* of attributes in the training set
- Ideally a few times per class

For $m$ attributes with $k$ possible values and $C$ classes, this means $O(Ck^m)$ instances


# Naive Bayes Solution

Assume different attributes are statistically independent, conditional on class

Compute $P(c|T)$ from $P(T|c)$ using Bayes rule

>[!example]
>You go to a shop you're pretty sure is open today, but when you get there all of the lights are off.
>
>What do you conclude?
>
>**Example numbers**:
>$P(\text{off}|\text{open}) = 0.01$
>$P(\text{off}|\text{closed}) = 0.85$
>$P(\text{on}| \text{open}) = 0.99$
>$P(\text{on}| \text{closed}) = 0.15$


>[!note] Bayes Rule
$$P(C,X) = P(C|X)P(X) = P(X|C)P(C)$$
>
>$$P(C|X) = \frac{P(X|C)P(C)}{P(X)}$$

## Naive Bayes Learner

**Task**: classify an instance T into one of the possible classes $c_j\in C$

Given an instance T (collection of attributes), what is the most likely class label?
$$\hat c = \arg \max_{c_j\in C}P(c_j|T)$$
Applying Bayes rule:
$$\hat c = \arg \max_{c_j \in C}P(T|C_j)P(c_j)$$

Classify an instance $T = \langle x_1, x_2, ..., x_n \rangle$

Naive bayes assumes all attributes are *independent*, conditional only on the class
- This makes the problems tractable, but is almost always untrue
- Despite this, it works well enough

So we go from this:
$$\hat c = \arg \max_{c_j\in C} P(x_1, x_2, ..., x_n|c_j)P(c_j)$$
(which is extremely difficult to compute because of the massive joint probability)

To this:
$$\hat c = \arg \max_{c_j \in C}\prod_{i}P(x_i|c_j)$$
due to the property:
$$P(x_1,x_2,...,x_n|c_j) = P(x_1|c_j)P(x_2|c_j)...P(x_n|c_j)$$
$\forall x_i$ are independent

### Bayesian Prior

The prior $P(c_j)$ is the likelihood of observing a given class
- Can be estimated from the frequency of classes in then training set (maximum likelihood estimate)


### Zero Values

If any $P(x_i|c_j) = 0$ , then the entire $P(c_j|T)$ becomes 0.

There are several *probabilistic smoothing* solutions

**Solution 1**:
The solution to this is typically picking a small value $\epsilon$
- This is essentially treating all unobserved combinations/events as unlikely
- This is another naive assumption (if we haven't seen it in training, it must be pretty unlikely)

$\epsilon$ should be *much* less than $\frac{1}{N}$ where $N$ = number of observed instances

Since $\epsilon$ is tiny, all probabilities still sum to 1


**Solution 2**
Slightly more complicated; increase *all* counts by 1
- *Laplace Smoothing*

Unseen events get a count of 1

A more general version is increasing all counts by $\alpha$, which is a value between 0 and 1.

Formula for attribute $X$ with $d$ values

| Unsmoothed              | Smoothed                                    |
| ----------------------- | ------------------------------------------- |
| $$P_i = \frac{x_i}{N}$$ | $$P_i = \frac{x_i + \alpha}{N + \alpha d}$$ |
### Missing Values
What if an instance is missing some attributes?

Missing values at test can simply be ignored - compute the likelihood of each class from the non-missing values

Missing values in training can also be ignored - don't include them in the attribute-class counts, and the probabilities will be based on the non-missing values.

