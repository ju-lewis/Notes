

## More Discrete Distributions

### Hypergeometric Distribution
In a population ($N$) with $D$ defective items, how many defective items are there in a sample (NO REPLACEMENT) of $n$?

Similar to binomial but without replacement
$$X \sim Hg(n, D, N)$$

**Remember!** $lim_{x \rightarrow \infty}{(1+\frac{x}{n})^n = e^x}$
### Poisson Distribution
Analogous to binomial distribution but as events happen over time.

$$N \sim Pn(\lambda)$$
$p_N(k)=\frac{e^{- \lambda} \lambda^k}{k!}$
$E(N)=\lambda$
$V(N) = \lambda$


**Deriving the Poisson Distribution from Bernoulli Trials**

Consider a sequence of $n$ Bernoulli trials performed over time.
Assume each of these trials takes a time of $\frac{1}{n}$ to complete

If the probability of a success is proportional to the time taken, $\mathbb{P}(\text{success}) = p = \frac{\lambda}{n}$, where $\lambda$ is a constant ($\lambda > 0$).
*We can think about $\lambda$ like a 'success rate' NOT PROBABILITY*

$$N \sim Bi(n, \frac{\lambda}{n})$$

We can then express compute the probability of a given number of successes over the $n$ trials as:
$$P(N=x)={n \choose x}(\frac{\lambda}{n})^x(1-\frac{\lambda}{n})^{n-x}$$
Expanding the expression for combinations:
$$P(N=x)=\frac{n!}{x!(n-x)!}(\frac{\lambda}{n})^x(1-\frac{\lambda}{n})^{n-x}$$
$$P(N=x)=\frac{n!}{x!(n-x)!}(\frac{\lambda^x}{n^x})(1-\frac{\lambda}{n})^{-x}(1-\frac{\lambda}{n})^{n}$$
As the 'time step' becomes infinitely smaller (i.e. as we approach a 'continuous' stream of trials) the number of trials grows too.

$$lim_{n \rightarrow \infty}\frac{n!}{x!(n-x)!}(\frac{\lambda}{n})^x(1-\frac{\lambda}{n})^{n-x} = \frac{\lambda^x}{x!}e^{-x}$$
So when we 'continuously' perform Bernoulli trials over $[0,1]$ with success rate $\lambda$
$$\mathbb{P}(N=x)=\frac{\lambda^x}{x!}e^{-x}$$

### Continuous Uniform Distribution
All values in an uncountable state space are equiprobable ($S_X \subseteq \mathbb{R}$)

Let $X$ be a random number chosen from a domain $[a,b]$
$$X \sim U(a,b)$$
$f_X(x)=\frac{1}{b-a}$
$F_X(x) = \int_{a}^{x}{\frac{1}{b-a}}dt = (x-a)\frac{1}{b-a}$

$E(X) = \frac{a+b}{2}$  The mean value!
$V(X) = \frac{(b-a)^2}{12}$

### Exponential Distribution
Analogous to geometric distribution for continuous random variables. Consider the waiting time for an event to occur.

Similarly to the geometric distribution - the exponential distribution has the *memoryless property*. (i.e. no matter how long you've waited so far, the probability of the event happening is still the same. $P(T-b > a | T > b) = P(T > a)$ )

$$X \sim exp(\alpha)$$
$f_X(x) = \alpha e^{-\alpha x} \ \ \ (\forall x \geq 0)$ 
$F_X(x) = 1 - e^{-\alpha x}$

$E(X) = \frac{1}{\alpha}$
$V(X) = \frac{1}{\alpha^2}$

Where $\lambda$ is the *rate of success* or the *rate parameter*.

### Mixed Distribution

A distribution is mixed if it contains any discontinuities, jumps (with the total jump size less than 1), and the remaining part is continuous.

### Gamma (Erlang) Distribution
Analogous to negative binomial distribution for continuous random variables.

$$Z \sim \gamma(r, \alpha)$$
Probability density and cumulative distribution functions:
$$f_Z(z) = \frac{\alpha^r z^{r-1}}{(r-1)!}(e^{-\alpha z}), z \geq 0$$
$$F_Z(z) = 1 - \sum^{r-1}_{k=0}{\frac{(\alpha z)^k}{k!}e^{- \alpha z}}$$
#### Gamma Function 
$$\forall x \in \mathbb{N}$$
$$\Gamma(x)=(x-1)!$$
**Note:**
$exp(\alpha) = \gamma(1, \alpha)$
(Remember the relationship between geometric and negative binomial)


$E(Z^k) = \frac{\Gamma(r+k)}{\Gamma(r)\alpha^k}$
$E(Z) = \frac{r}{\alpha}$ (number of occurrences * (1/rate parameter))

$V(X) = \frac{r}{\alpha^2}$

### Beta Distribution
Useful for quantitative phenomena with observed values bounded by a certain interval, where it is unreasonable to assume the quantities take values equally likely.
$$X \sim Beta(\alpha, \beta)$$
$f_X(x) = \frac{x^{\alpha - 1}(1-x)^{\beta - 1}}{B(\alpha, \beta)}$
Where
$$B(\alpha, \beta) = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha + \beta)}$$

$E(X) = \frac{\alpha}{\alpha + \beta}$
$V(X) = \frac{\alpha \beta}{(\alpha + \beta)^2(\alpha + \beta + 1)}$

