
## Applications of Cumulant Generating Function

Using our *cumulant generating function* $K_X(t) = ln(E(e^{tX}))$ we can compute the *cumulants*:

Recall that we can use the *Taylor expansion* $K_X(t)$:
$$K_X(t) = \sum_{r=1}^{\infty}\frac{\kappa_rt^r}{r!}$$

>[!note]
>Generally, the cumulant formula is:
>$$\kappa_r = K_X^{(1)}(0)$$

**Important Cumulants**:
- $\kappa_1 = K_X^{(1)}(0) = E(X)$
- $\kappa_2 = K_X^{(2)}(0) = Var(X)$
- $\kappa_3 = K_X^{(3)}(0) = E(X^3)-3E(X)E(X^2)+2E(X)^3$ *skewness*
- $\kappa_4 = K_X^{(4)}(0) = E((X-E(X))^4)-3\sigma^4$ *kurtosis*

### Skewness
Skewness reflects the level of symmetry of the distribution about its mean

A symmetrical detail has a skewness of $0$

**Removing Scaling**:
$$\text{skew}(x) = \frac{\kappa_3}{\sigma^3}$$
### Kurtosis
Kurtosis is a measure of how 'flat' the distribution is
- Positive kurtosis -> tall
- Negative kurtosis -> flat

$$\text{kurt}(x) = \frac{\kappa_4}{\sigma^4}$$
## Laplace Transform

$$L_X(t) = M_X(-t) = E(e^{-tX})$$

Note that the Laplace transform exists for all $t \gt 0$
### Inversion Formula for Laplace Transformations

The Laplace transformation can easily be inverted to recover the distribution function
$$F_X(x)=\lim_{t \to \infty}\sum_{k \leq tx}\frac{(-t)^k}{k!}L_X^{(k)}(t)$$

## Recovering Distribution from Generating Functions

**Discrete Case**:
Remember that $P_X(z) = \sum_{i=0}^{\infty}z^ip_X(i)$, so we can 'read off' the probabilities if the form is a polynomial of $z$

Otherwise, we can continually differentiate with respect to $z$, and substitute in $z=0$ for each derivative to obtain the probabilities.

**Continuous Case**:
- If the RV is non-negative, we can convert the *mgf* to the Laplace transform and invert the distribution from there
- In general, convert to the related *characteristic function* and invert from there


### Characteristic Function
$$g_X(t) = E(e^{itX})$$
If $X$ is a continuous random variable:
$$g_X(t) = \int^{\infty}_{-\infty}e^{itX}f_X(x)dx$$

This is the *Fourier Transform* of the pdf $f_X$

As the Fourier Transform is, in a sense, self-inverse:
$$f_X(x)=\frac{1}{2 \pi}\int_{-\infty}^{\infty}e^{itX}g_X(t)dt$$
This "inversion formula" allows us to recover the distribution from the characteristic function
- When using the characteristic function instead of the MGF, we don't need to worry about the behaviour of the moments - it'll always be defined


## Convergent Distributions

>[!note]
>If the MGF converges, the distribution converges


### Law of Large Numbers

For some $S_N = X_1 + X_2 + ... + X_n$,
$$\frac{S_n}{n} \to {\!\!\!\!\!\!\!^d} \mu$$
*The mean of all of the experiments approaches the individual trial mean*
Note that for this to make sense, we're interpreting $\mu$ as a random variable that is constant with probability 1
### Central Limit Theorem

The sum of many random variables is approximately normally distributed with:
$$S_N \approx {\!\!\!\!\!^{^d}} N(n\mu, n\sigma^2)$$

And the mean is approximated by:
$$\bar X \approx {\!\!\!\!\!^{^d}} N(\mu, \frac{\sigma^2}{n})$$


## Stochastic Processes

If we consider a series of random variables happening across time:
$S$ is the state space
$T$ is the time set

$X(t)$ or $X_t$ denotes a single random variable $X$ (indexing the stochastic process with time)

### Poisson Process
Discrete-space, continuous-time analogue of a sequence of Bernoulli trials
- $X(t)$ describes the number of "points" that occur in time $[0,t]$

Poisson process allows us to consider poisson RVs with changing time bounds

For some fixed $t$:
- The number of events has a Poisson distribution: $\text{Pn}(\alpha t)$
- The waiting time until the first event has distribution: $\text{Exp}(\alpha)$
- The waiting time until the $r$th event has a distribution: $\text{Gamma}(r, \alpha)$

### Discrete Time-Homogeneous Markov Chains


