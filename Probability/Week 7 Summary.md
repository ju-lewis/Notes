

## Bivariate Random Variables


### Discrete Bivariate Random Variables

**Probability mass function**

**Continuous distribution function**

**PMF -> CDF**
The CDF at $(x_0, y_0)$ is the sum of all 'points' on the X-Y plane where $x \leq x_0, y \leq y_0$

We express the CDF as a large piecewise function describing all domains for distinct values of the CDF (where the domains are rectangles with their bottom left corner at $(-\infty, -\infty)$ )

This can be incredibly time consuming as you have to carefully consider all possible domains that include a given amount of points (e.g. have a given cumulative probability)

**CDF -> PMF**
To obtain a PMF from a bivariate CDF, we can subtract rectangular domains to 'single out' the square we want.

*Process*
- Consider the 2D state space as a (discrete) grid - each intersection represents the PMF at the given point $(x,y)$

|        |        |        |     |
| ------ | ------ | ------ | --- |
| p(1,3) | p(2,3) | p(3,3) |     |
| p(1,2) | p(2,2) | p(3,2) |     |
| p(1,1) | p(2,1) | p(3,1) |     |
If we want to compute $\mathbb{P}(X=3,Y=3)$, we can use cumulative probabilities like so:
$$p(3,3)=F(3,3)-F(2,3)-F(3,2)+F(2,2)$$
So we take the cumulative probability at $(3,3)$, and subtract the previous cumulative probabilities to *isolate* $\mathbb{P}(X=3,Y=3)$. (Remember to add back the region that is subtracted twice - i.e. $F(x-1,y)\cap F(x, y-1)$)

More generally:
$$p(x,y) = F(x,y) - F(x-1,y) - F(x, y-1) + F(x-1, y-1)$$

### Continuous Bivariate Random Variables

Continuous bivariate random variables have a *bivariate probability density function*

**Computing cumulative probability**
$$F(x,y) = \int^{b}_{a}{\int^{d}_{c}{f(x,y)} \ dx} \ dy$$
Remember, order of integration can be changed according to Fubini's theorem!


