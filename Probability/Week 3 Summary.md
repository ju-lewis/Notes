
## Continuous Random Variables

A random variable is continuous if its *state space* is uncountable

Continuous random variables do **not** have point probability masses, instead they have a *probability density function*.
Probability density function = $f_X(x)$

$P(a < X < B) = \int^{b}_{a}{f_X(x)}dx$

A continuous random variable's *probability distribution function* is given by:
$F_X(x)=\int^{x}_{-\infty}{f_X(x)}dx$

## Probability Distribution Functions

A function $F_X(x)$ is a probability distribution function of random variable $X$ if:
1. $F_X$ is non-decreasing (as all probabilities must be greater than 0)
2. $0 \leq F_X(x) \leq 1$
3. $F_X(x)$ is right-continuous

## Expectation and Variance

For a discrete random variable $X$:
$\mathbb{E}(X) = \sum_{x\in S_X}{x p_X(x)}$

For a continuous random variable $X$:
$\mathbb{E}(X) = \int^{\infty}_{-\infty}{x f_X(x)}dx$

The variance is the *mean difference from the mean all squared*
$\mathbb{V}(X) = E(X - E(X))^2$