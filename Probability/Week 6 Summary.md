
## More Continuous Distributions

### Pareto Distribution
*Very* heavy-tailed analogue to the exponential distribution

$$X \sim \text{Pareto}(\alpha, \gamma)$$
$\alpha$ describes the 'starting point' (as $x \geq \alpha$)
$\gamma$ is the *decay rate* ($\gamma > 0$)

*How does it increase tail probability?*
- The distribution is no longer exponential, rather a *power function*

$$F_X(x) = 1-(\frac{\alpha}{x})^{-\gamma}$$
 Pareto distribution tail is sometimes so large that $E(X)$ doesn't converge
- This also applies to higher moments
- We can intuitively see this by integrating the tail function: $\int_{0}^{\infty}{(\alpha/x)^{-\gamma}}dx$ this will only converge under specific conditions


### Weibull Distribution
Combination of exponential distribution and a polynomial function.

$$X \sim \text{Weibull}(\beta, \gamma)$$

*How does it increase tail probability?*
- Dividing $x$ by a factor ($\beta$) to decrease decay rate

$$F_X(x) = 1 - e^{-(x/\beta)^\gamma}$$

### Normal Distribution
Good approximation of many distributions

$X \sim N(\mu, \sigma^2)$

### Cauchy Distribution
The Cauchy distribution describes the x-intercept of a ray originating from $(x_0, \gamma)$ with a uniformly distributed angle.

$F_X(x) = \frac{1}{\pi} \text{arctan}(\frac{x-x_0}{\gamma})+\frac{1}{2}$

### Lognormal Distribution
Transformation of *normal distribution*


$\text{Let }X \sim N(\mu, \sigma^2), \ Y = e^X$
$$F_Y(y) = P(Y < y) = P(e^X < y) = P(X < log(y)) = F_X(log(y))$$
So, $Y \sim LN(\mu, \sigma^2)$

>[!note] NOTE
>Mean $\ne \mu$
>Variance $\ne \sigma^2$

## Transformations

We can define a random variable as a function of another, effectively *transforming* one variable to another.

*Usual process*:
1. Define $Y$ in terms of $X$
2. Express $F_Y(y)$ as a probability statement (e.g. $P(Y < y)$)
3. Use definition of $Y$ in terms of $X$ to rearrange $F_Y(y)$ until we get $F_X(...)$

We use the *cumulative distribution function* as it provides a simple abstraction allowing us to relate random variables to values - without having to expand the underlying functions.

This doesn't matter with discrete random variables as we can just as easily use the *probability mass function* ($p_Y(y) = P(Y = y)$), but this isn't an option with continuous RVs.



