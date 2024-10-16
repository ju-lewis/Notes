
>[!note]
>This exam is going to be read in class by the lecturer anyway, so I thought I'd use it to take notes on exam format/challenge


## Question 1
*Topic:* Axioms of Probability

1ai. **Easy**
	disjoint $\implies A \cap B = \emptyset$ 
1aii. **Easy**
	exhaustive $\implies A \cup B = \textbf{A}$ 

1b. **Easy (with notes)**
	Probability is always non-negative, $P(\Omega) = 1$, For disjoint events $A$, $B$; $P(A+B) = P(A) + P(B)$

1c. **Easy**
	$P(\{\omega_1, \omega_2, ..., \omega_n\}) = 1$
	All outcomes are disjoint
	$P(\omega_1) + P(\omega_2) + ... + P(\omega_n) = 1$
	All probabilities are equally likely, so:
	$n\times P(\omega_i) = 1 \text{ for any } i \in 1,...,n$
	So
	$P(\omega_i) = \frac{1}{n}$

1d.
	$A \subset \Omega$, hence A is a set of outcomes
	all outcomes have the same probability, and there are $\#A$ of them


## Question 2
*Topic*: Conditional probability 

2a: **Easy**
	Bayes' formula:
	$$P(A_i|H) = \frac{P(A_i)P(H|A_i)}{\sum_{j}P(H|A_j)P(A_j)}$$
2bi: **Easy**
	Determine $P(A_1|A_1 \cap A_2 \cap A_3) = \frac{P(A_1)}{P(A_1 \cap A_2 \cap A_3)}$
	the other 2 sub-parts are essentially the same

2bii: **Easy**
	P(defaults) = 1/50 * 0.3 + 1/25 * 0.25 + 1/20 * 0.25

2biii: **Easy**
	P(defaults | $A_3$) = $\frac{P(\text{defaults}, \ A_3)}{P(A_3)}$


## Question 3:
*Topic*: Continuous random variables (and transformation ?)

3a: **Easy**
	$S_X = [0, 2]$, $S_Y = [1, e^2]$

3b: **Easy**
	$F_X(x) = \frac{x}{2}$
	$f_X(x) = \frac{1}{2}$

3c: **Easy**
	$E(X) = \frac{0 + 2}{2} = 1$
	$V(X) = \frac{(2-0)^2}{12} = \frac{1}{3}$

3d: **Easy**
	$F_Y(y) = P(Y \leq y) = P(e^X \leq y) = P(X \leq \ln(y)) = \frac{\ln(y)}{2}$
	$f_Y(y) = \frac{d}{dy}(\frac{\ln(y)}{2}) = \frac{1}{2y}$

3ei: **Easy**
	$E(Y) = \int_{S_X}e^xf_X(x)dx = \frac{1}{2}[e^x]^{2}_0 = \frac{1}{2}(e^2-1)$

3eii: **Easy**
	$E(Y) = \int_{S_Y}yf_Y(y)dy = \frac{1}{2}[1]^{e^2}_{1} = \frac{1}{2}(e^2-1)$

3f: **Easy**
	First calculate $E(Y^2)$
	Then compute $V(Y) = E(Y^2) - E(Y)^2$

3g: **Easy (with notes)**
	Let $\mu = E(X)$, $\sigma^2 = V(X)$
	$E(Y) \approx e^\mu + e^\mu E(X-\mu) + \frac{1}{2}e^\mu E((X-\mu)^2)$
	$V(Y) \approx e^\mu \mu^2 \sigma^2$


## Question 4
*Topic*: Application of special probability distributions (and Poisson processes)

*Notes*:
- Strange notation $N^N(t)$ referring to number of northbound trains
	- $N^S(t)$ is number of southbound train

4a: **Easy**
	We know $N^N(t) \sim Pn(\lambda_1 t)$
	$p_{N^N(t)}(n) = \frac{e^{-\lambda_1 t}(\lambda_1 t)^n}{n!}$

4b: **Moderate ?**
	$E(N^N(t)) = \sum_{n \in S_{N^N(t)}}(n)\frac{e^{-\lambda_1 t}(\lambda_1 t)^n}{n!}$
	Just work out what this sum equates to
	*we can check the value using the known expectation of a Poisson RV*: $E(N^N(t)) = \lambda_1 t$

4c: **Easy**
	The total number of trains will simply be the sum of southbound and northbound
	Applying the law of total probability:
$\ \ \  \ \ \ \ \ P(N(t) = k) = P(N^N(t) + N^S(t) = k) = \sum_{n \in S_{N^N(t)}}P(N(t) = k | N^N(t) = n)P(N^N(t) = n)$
	$= \sum_{n=0}^\infty P(N^S(t)=k-n)P(N^N(t)=n)$ 
	Since $N^N(t)$ and $N^S(t)$ are independent
	This then becomes pretty easy to evaluate

4d: **Easy**
	Exponential distribution
	$F_{N^N(T)}(t) = 1-e^{\lambda_1 t}$
	The note about $\{N^N(t) = 0\}$ being the same as $\{T > t\}$ means 0 northbound trains arriving between $0$ and $t$ means the first arrival time $T$ must be greater than $t$

4e: **Easy**
	Using the memoryless property of exponential distributions
	...

## Question 5
*Topic*: continuous bivariate random vectors

5a: **Easy (with notes)** 
	$S_X = \{x \ | \ 0 \leq x \leq \frac{2-y}{2}\}$
	$S_Y = \{y \ | \ 0 \leq y \leq 2(1-x)\}$



