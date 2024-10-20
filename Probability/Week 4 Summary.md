## Moments

The $n^{th}$ moment of a random variable $X$ is expressed as:
$$\mu_n(X) = \mathbb{E}(X^n)=\sum_{x \in S_X}{x^n p_X(x)}$$

Computing moments using *tail probabilities*
$$E(X^n) = n\int_{0}^{\infty}{x^{n-1}(1 - F_X(x))}dx$$


## Discrete Random Variable Distributions

### Binomial Distribution
How many successes are there in $n$ trials?
$$X \sim Bi(n, p)$$
$p_X(x) = {n \choose x}(p)^x(1-p)^{n-x}$

This formula is intuitive:
- $p^x$ is the probability that you have $x$ successes occur
- $(1-p)^{n-x}$ is the probability that the rest of the trials were failures
- $n \choose x$ is the number of ways this could have occurred

$E(X) = np$
$V(X) = np(1-p)$
### Geometric Distribution
How many failures before there is a success?
$$N \sim Ge(p)$$

$p_X(x)=(1-p)^xp$

$E(X) = \frac{1-p}{p}$
$V(X) = \frac{1-p}{p^2}$

**Proof**:
$E(N) = \int^{\infty}_{0}{(1-F_N(x))}dx$ (Using tail probabilities)
$E(N) = \sum^{\infty}_{i=0}{\int^{i+1}_{i}{P(N > x)}}dx$
$E(N) = \sum^{\infty}_{i=0}\int^{i+1}_{i}{q^{i+1}}dx$
$E(N) = \sum^{\infty}_{i=0}{q^{i+1}}$
$E(N) = \frac{q}{1-q}$
$E(N) = \frac{1-p}{p}$


### Negative Binomial Distribution
How many failures before there are $r$ successes?
$$Z \sim Nb(r, p)$$
$E(X) = \frac{r(1-p)}{p}$
$V(X) = \frac{r(1-p)}{p^2}$

This is very closely related to the binomial distribution, and can be translated to an equivalent binomial expression:

What is the probability of $a$ failures before $b$ successes?
*is equivalent to*
What is the probability that there are $b$ successes in $a+b$ trials?

As the 'worst case' for a negative binomial distriu

