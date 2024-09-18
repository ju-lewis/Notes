## Standard Bivariate Normal Distribution

$$(X, Y) \sim N_2(\rho)$$

$\rho > 0 \implies$ X and Y 'help' each other (*positive relationship*)
$\rho < 0 \implies$ X and Y 'work against' each other (*negative relationship*)

$$\rho \text{ is the correlation coefficient.}$$

If $\rho$ is 0, the PDF's contour plot forms a set of concentric circles


## General Bivariate Normal Distribution

$$(X, Y) \sim N_2(\rho, \mu_1, \mu_2, \sigma_X, \sigma_Y)$$
$X \sim N(\mu_X, {\sigma_X}^2)$
$Y \sim N(\mu_Y, {\sigma_Y}^2)$

$X$ and $Y$ are independent *if and only if* $\rho = 0$, as $\rho$ describes the correlation between the 2 variables.

We can standardise each marginal distribution as normal:
$X_s \sim N(0, 1) = \frac{X-\mu_X}{\sigma_X}$
$Y_s \sim N(0, 1) = \frac{Y-\mu_Y}{\sigma_Y}$

We can use this to more easily compute transformed or continuous distributions of $(X,Y)$

$$(X_s|Y_s=y_s) \sim N(y \rho, 1-y \rho^2)$$

## Expectation of Bivariate Functions

As with functions of a univariate random variable, we can compute the expectation as follows:

**Discrete Case**:
$$E(\psi(X,Y)) = \sum_{S_{(X,Y)}}{\psi(x,y)p_{(X,Y)}{(x,y)}}$$


**Continuous Case**:
$$E(\psi(X,Y)) = \int_{S_{(X,Y)}}{\psi(x,y)f_{(X,Y)}{(x,y)}}dxdy$$

## Distributions of Bivariate Transformations



Consider a transformation of a bivariate distribution $G = \psi(X, Y)$

$$F_G(g) = P(\psi(X,Y) \leq g)$$
How can we break down $\psi(X,Y)$ into distributions we already know? - Using conditional probability (*Law of Total Probability*)

If we consider the shared state space to be partitioned by the values of $X$, then:

**Discrete Case**:
$$F_G(g) = \sum_{x \in S_X}{P(\psi(x,Y) \leq g \ | \ X = x)}P(X = x)$$

**Continuous Case**:
$$F_G(g) = \int_{S_X}{P(\psi(x,Y) \leq g \ | \ X = x)}f_X(x)dx$$
As we've conditioned $\psi(X,Y)$ on $X$ taking the value $x$, we have effectively removed one random variable from the equation - as we're using the *law of total probability* to consider all possible instances of $X$ (and their corresponding likelihood).

This means we can compute the inverse function of $\psi$ allowing us to transform the expression:
$$P(\psi(X,Y) \leq g \ | \ X = x)$$
to isolate $Y$ in the form:
$$P(Y \leq \ ... \ | \ X = x)$$
Now we have an expression only dependent on the *marginal distributions*

>[!note]
>If the random variables are independent it becomes *even easier* as we have:
>
>$P(Y \leq \ ... \ | \ X = x) = P(Y \leq \ ...)$
>
>So the overall expression becomes something of the form
>
>$$F_G(g) = \sum_{x \in S_X}{P(Y \leq \ ...)P(X = x)}$$
>
>Where the instance of $Y$ is a kind of inverse application of $\psi$





