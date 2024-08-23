

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

### Exponential Distribution
Analogous to geometric distribution for continuous random variables. Consider the waiting time for an event to occur.



