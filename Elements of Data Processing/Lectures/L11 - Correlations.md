

## What is Correlation?
Correlation is used to detect pairs of variables that might have some kind of *relationship*


**Correlation Strength**
How close do the points fit to the observed trend?

Correlations can be non-linear (quadratic, piece-wise linear, etc.)

Remember, correlation =/= causation


### Why is correlation important?
- Helps us discovery relationship
- A step towards discovering causality
	- Example: Smoking causes lung cancer
- Feature ranking (for building better predictive tool)
	- A good feature to use is a feature with high correlation to the one we're trying to predict.


### Pearson Correlation
Null-correlation => one variable doesn't change while the other does (obvious relation)
No correlation => Points are very scattered, no obvious relation


**Problems with Euclidean distance**
- Objects can be represented with different measure scales (e.g. days doesn't scale the same way as number of sales)
- Lose directionality


We define a correlation measure $r_{xy}$, assessing samples from two features $x$ and $y$
- Assess how close their scatter plot is to a straight line.

**Categorising Pearson Correlation**
(Note: it usually depends on what your data is)
- 0.5 => large
- 0.3-0.5 => moderate
- 0.1-0.3 => small
- 0.1 => trivial

*An example of why this varies:*
For a social science experiment (e.g. something about human behaviour), 0.5 correlation could be massive.
For an engineering experiment, with the relationships between variables being well-defined by mathematical expressions, we would expect far higher correlation.


**Properties**:
- Range within \[-1, 1\]
- Sensitive to outliers
- Can only detect linear relationships
- Scale invariant
- Location invariant

>[!tldr]
How well do the points approximate a straight line?


## Mutual Information


### Entropy
Used to quantify the uncertainty in an outcome.

Randomly select from the 2 sets:
{1,1,1,1,1,1,2,2}
{1,2,3,5,6,7,8,9}
Which one are we more sure about the outcome of?

High uncertainty => high entropy
Low uncertainty => low entropy

**Quantifying entropy:**
For $k$ possible outcomes:
$$H(X) = -\sum^{k}_{i=1}{p_i log_2p_i}$$


