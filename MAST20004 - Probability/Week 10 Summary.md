

## Approximation

It's not always easy to compute expectation directly (depending on $\psi$):
$$E(\psi(X))=\int_{S_X}\psi(x)f_X(x)dx$$
So we can use approximations instead.

One approach to doing this is using the Taylor series expansion of $\psi$ around $E(X)=\mu$

$$\psi_{\mu}(X) \approx \sum_{k=0}^{\infty}{\frac{\psi^{(k)}(\mu)}{k!}(X-\mu)^k}$$

We can acceptably use a second order expansion
### Approximating Expectation
$$E(\psi(X)) \approx E( \ \psi(\mu) + \psi'(\mu)(X-\mu))+\frac{1}{2}\psi''(\mu)(X-\mu)^2 \ )$$
$$E(\psi(X)) \approx \psi(\mu) + \psi'(\mu)E(X-\mu) + \frac{1}{2}\psi''(\mu)E((X-\mu)^2)$$

### Approximating Variance
In a similar way, we can also use the Taylor expansion to approximate the variance
- Here, we can use use a first order Taylor approximation
$$V(\psi(X)) \approx \psi'(\mu)^2\sigma^2$$

## Bienayme's (Chebyeshev's) Inequality

$$P(\frac{|X-\mu|}{\sigma} \geq k) \leq \frac{1}{k^2}$$
Instances of a random variable become less and less likely the further they are from the mean.

## Generating Functions

### Overview

Generating functions unique describe a probability distribution.
- They can be thought of like an *encoding* of the distribution

### Probability Generating Function
For a non-negative integer-valued discrete random variable

$$P_X(z)=\sum_{i=0}^{\infty}{z^ip_X(i)}$$
From this we can derive some properties:
1. $P_X(1) = \sum_{i=0}^{\infty}p_X(i) = 1$
2. $P'_X(1)=\sum_{i=1}^{\infty}{i(1)^{i-1}p_X(i)} = E(X)$

If the PGF is a simple polynomial (e.g. $P_X(z) = 1 + 0.1z + 3z^2 + 4z^3$)
We can just 'read off' the PMF of X, as they'll be the coefficients of the powers of $z$

### Moment Generating Function
For a continuous function, it's often easier to use the *moment generating function* (MGF)

$$M_X(t)=E(e^{tX})$$

We can convert the PGF to a MGF through the relation:
$$M_X(t)=P_X(e^{t})$$

### Central Moment Generating Function
### Cumulant Generating Function
If we have a random variable defined as the sum of *independent* random variables:
$$S_N=X_1+X_2+X_3+...+X_n$$
Taking the MGF will result in the following expression:
$$M_{S_N}(t) = E(e^{tX_1+tX_2+...+tX_n}) = E(e^{tX_1}e^{tX_2}...e^{tX_n})$$
$$M_{S_N}(t)=E(e^{tX_1})E(e^{tX_2})...E(e^{tX_n})$$

We can convert this into a sum by taking the natural log:
$$K_{S_N}(t)=\ln(M_{S_N}(t))=\ln(E(e^{tX_1}))+\ln(E(e^{tX_2}))+...+\ln(E(e^{tX_n}))$$









