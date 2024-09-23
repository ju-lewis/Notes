
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


## Covariance and Correlation

$$\text{cov}(X,Y) = E(XY)-E(X)E(Y)$$
$$\text{cov(X, Y)} = E[(X-\mu_X)(Y-\mu_Y)]$$


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



## Conditioning on an Event




### Conditional Expectation

$$\eta(Y) = E(X \vert Y) \ \ \ \text{ Is a random variable}$$

$E(\eta(Y)) = E(E(X \vert Y)) = E(X)$




### Conditional Variance

$V(\eta(Y)) = E(\eta(Y)^2) - E(\eta(Y))^2$
$\ \ \ \ \ \ \ \ \ \ \ \ \ \  =E(\eta(Y)^2)-E(X)^2$ Using our previous identity


$V(E(X \vert Y)) + E(V(X \vert Y)) = V(X)$

