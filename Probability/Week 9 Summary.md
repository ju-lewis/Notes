
## Bivariate Distributions - Continued

### The Convolution Formula

Given a distribution $G = \psi(X,Y)$, a common occurrence is the form $G = X + Y$ (where $X$ and $Y$ are independent), in this case we can use the law of total probability to derive the CDF and PMF/PDF of $G$:

>[!note] 
>Keep in mind the geometrical interpretation of the random variable $G = X + Y$, and how graphing $Y$ against $X$ yields a straight line with intercepts at the instance of $G$. (as $Y = G - X$)

**Discrete Case:**
$$p_G(g) = \sum_{i=0}^{g}{p_X(i)p_Y(g-i)}$$



**Continuous Case:**

We know that the *cumulative* probability will be the double integral over the 'triangle' formed bounded by the line $y = g - x$
$$F_G(g) = \iint_{\{(x,y) : x+y \leq g\}}{}f_{X,Y}(x,y)dxdy$$

## Conditional Distributions

If two random variables 'have an effect' on each other, then it makes sense to look at how the distribution of one of them changes based on the value of the other. 

i.e. $P(X = x | Y = y)$, where the value of $Y$ is known to be equal to $y$.

In this case we say we're *conditioning* on $Y$


Much like considering conditional probabilities, conditional distributions are computed as follows:
$$p_{X|Y}(x|y) = \frac{p_{X,Y}(x,y)}{p_Y(y)}$$
$$f_{X|Y}(x|y) = \frac{f_{X,Y}(x,y)}{f_Y(y)}$$

This implies that we can examine the meaning of *independence of distributions*.

$X$ and $Y$ are independent if and only if:
$$p_X(x) = p_{X|Y}(x|y) = \frac{p_{X,Y}(x,y)}{p_Y(y)}$$
$$p_{X,Y}(x,y) = p_X(x)p_Y(y)$$
(This of course extends to continuous random variables)



## Covariance and Correlation

$$\text{cov}(X,Y) = E(XY)-E(X)E(Y)$$
$$\text{cov(X, Y)} = E[(X-\mu_X)(Y-\mu_Y)]$$


$\text{Independence } \implies \text{cov}(X, Y) = 0$
$\text{cov(X,Y) = 0} \ \ \not \! \! \! \implies \text{ independence}$


>[!note]
>Recall that if $X$ and $Y$ are independent, $E(XY) = E(X)E(Y)$
>
>It is also true that $V(X+Y) = V(X) + V(Y)$


### Variance-Covariance Matrix
$$
\begin{bmatrix}
	{\sigma_x}^2 & \rho \sigma_x \sigma_y \\
	\rho \sigma_x \sigma_y & {\sigma_y}^2
\end{bmatrix}
$$


### Correlation


$$\rho = \frac{\text{Cov}(X,Y)}{\sqrt{V(X)V(Y)}}$$

**Properties of Correlation:**
- $|\rho| < 1$


## Conditioning on an Event

We have already seen how we can condition a random variable $X$ based on the value of another random variable $Y$, for example: $p_{X|Y}(x|y) = P(X = x | Y = y)$


We can extend this to a more general notion of conditioning on *an event*.
For example:
$$P_{X|A}(x) = P(X = x | A) = \frac{P(\{X = x\} \cap A)}{P(A)}$$

$$F_{X|A}(x) = P(X \leq x \ | \ A) = \frac{P(\{X \leq x\} \cap A)}{P(A)}$$

**Expectation**
Discrete:
$$E(X|A) = \sum_{x \in S_X}{xP(X=x|A)}$$
Continuous:
$$E(X|A) = \int_{-\infty}^{\infty}xf_{X|A}(x)dx$$

**Variance**:
$$V(X|A) = E(X^2|A) - E(X|A)^2$$

## Conditioning on a Random Variable



### Conditional Expectation

We can easily compute the expected value of $X$, given $Y$ takes a known value
- This is simply conditioning on the value of $Y$
$$\eta(y) = E(X \vert Y = y) := \sum_{x \in S_X}{x p_{X|Y}(x|y)}$$


We can express the *conditional expectation* of $X$ given $Y$ as $Z = \eta(Y)$
- $Z$ is a random variable
- We can also write $Z = E(X|Y)$

![[conditional-expectation.png]]


Since the distribution of $E(X|Y)$ is dependent on $Y$, $P(E(X|Y) = \eta(y)) = p_Y(y)$


>[!note]
>If $Y$ is discrete, $E(X|Y)$ takes value $\eta(y)$ with probability $p_Y(y)$


### Conditional Variance


In the same way we can examine the expectation of $X$ given that $Y$ has taken a value $y$, we can look at the effect of conditioning variance on $Y$:

$$v(y) = V(X|Y=y) = E(X^2|Y=y)-E(X|Y=y)^2$$
**Discrete Case**
$$E(X|Y=y)=\sum_{x\in S_X}xp_{X|Y}(x|y)$$
$$E(X^2|Y=y)=\sum_{x\in S_X}x^2p_{X|Y}(x|y)$$
**Continuous Case**
$$E(X|Y=y)=\int_{-\infty}^{\infty}{xf_{X|Y}(x|y)}dx$$
$$E(X^2|Y=y)=\int_{-\infty}^{\infty}{x^2f_{X|Y}(x|y)}dx$$



$V(\eta(Y)) = E(\eta(Y)^2) - E(\eta(Y))^2$
$\ \ \ \ \ \ \ \ \ \ \ \ \ \  =E(\eta(Y)^2)-E(X)^2$   Using our previous identity


>[!example] Important Identities
>#### Law of Total Expectation
$E(\eta(Y)) = E(E(X \vert Y)) = E(X)$
>#### Law of Total Variance
> $V(E(X \vert Y)) + E(V(X \vert Y)) = V(X)$

