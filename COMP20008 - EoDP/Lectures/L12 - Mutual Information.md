

## Properties of Entropy

$$H(X) = -\sum^{}_{}p_ilog_2(p_i)$$


Entropy is always non-negative
$$H(X) \geq 0$$

Entropy is *maximised* for a uniform distribution (highly uncertain about what is likely to be picked)



### Variable Discretisation

Continuous features must first be categorised into *bins*.

>[!example]
>Transforming floating point value to `small`, `medium`, and `large` for size

#### Techniques


**Equal-width binning**
	Divide the range of the continuous feature into equal length intervals (bins).
	e.g. intervals of 10 (any value within that range goes in the bin)

**Equal-frequency binning**
	Divide range of continuous feature into bins containing equal numbers of values
	e.g. place first 10 in 1st bin, next 10 in 2nd bin


Domain knowledge allows us to assign thresholds manually:
Car speed example:
- 0-40km/h -> slow
- 41-80km/h -> medium
- 81+ km/h -> fast


## Mutual Information


### Conditional Entropy
How does entropy change when we filter results by a predicate?

![[conditional-entropy.png]]

For example, if we know someone wears glasses, the entropy is *drastically* reduced.


$$H(Y|X) = \sum_{x \in X}p(x)H(Y|X=x)$$
We simply sum the entropy of `Y` for all of the "states of `X`"

Mutual information is a measure of correlation
- The amount of information about Y we gain by knowing X
- The amount of information about X we gain by knowing Y



**Classifying Mutual Information**
Large MI -> highly correlated
Small MI -> not very correlated

We can normalise mutual information, as it's always non-negative (and unbounded)


>[!note] Property of conditional entropy:
>$$0 \leq MI(X, Y) \leq min(H(X), H(Y))$$

So we can normalise MI by dividing by:
- Min
- Max
- Mean


![[pearson-vs-nmi.png]]

**Advantages**
- Can detect linear and non-linear dependencies
- Applicable for discrete features
**Disadvantages**
- If feature is continuous, it must be discretised
- Not always obvious how binning should be done



