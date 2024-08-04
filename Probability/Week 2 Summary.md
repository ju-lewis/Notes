
## Conditional Probability

### Independence of 2 Events
The probability of A occurring *given* B already occurred is expressed as follows:
$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$
Two events $A$ and $B$ are *independent* if $P(A|B) = P(A)$, i.e. if the chance of $A$ occurring is unaffected by B. This means that if $A$ and $B$ are disjoint, they cannot be independent unless $P(A) = 0$

If two events are independent then $P(A \cap B) = P(A)P(B)$ 

### Mutual Independence of $n$ Events
In order to prove that a set of $n$ events is mutually independent, we must check that all subsets of events are independent.

e.g. for 3 events A, B, and C we must establish the independence of:
(A, B), (A, C), (B, C), (A, B, C)

The number of subsets grows proportionally to $2^n$ and thus quickly becomes incomputable.

We likely won't be told to determine the mutual independence of more than 3 events.

## Bayesian Probability

**Law of complete probability:**
$$P(H) = \sum_{i}{P(H | A_i)P(A_i)}$$
The law of complete probability tells us that if we know the probability of a result occurring because of specific (probabilistic) causes, we can determine the overall probability of the event H occurring.


**Bayes' Formula:**
$$P(H|A_i) = \frac{P(H|A_i)P(A_i)}{\sum_{j}P(H|A_j)P(A_j)}$$
This equation tells us how to compute the probability of a given 'cause', given the probabilities of the overall event (H) occurring.


## Random Variables

A *random variable* is a mapping: $\Omega \mapsto \mathbb{R}$

We can think about a random variable like a layer of abstraction over the probabilities of outcomes in $\Omega$, allowing us to express more complex ideas.

The set of values that can be represented by a random variable $X$ is $S_X \subseteq \mathbb{R}$

>[!example]
>We can define a *discrete random variable* $X$ to be the number of heads observed when we flip 2 coins.
>
>The sample space of this random experiment is quite easy to express:
>
>$\Omega = \{(H, T),(H, H),(T,H),(T,T)\}$
>
>So in this case, $X$ maps a given tuple in the sample space to the number of occurrences of '$H$' in the tuple.
>
>For instance, we can compute $P(X = 2) = P((H, H))$ = $\frac{1}{4}$

$P(X = x)$ is commonly used as a shorthand for $P({\omega: X(\omega) = x})$ but the second form more explicitly shows the mapping from an event to a real number.

### Discrete Random Variables

A random variable is discrete if its *state space* is countable.

For a discrete random variable $X$, its probability mass function is:
$$p_X(x): S_X \mapsto \mathbb{R} = P(X=x)$$

>[!info]
>So the probability of a discrete random variable taking a given value is that value's *probability mass.*


We can now compute the probability of a random variable $X$ taking on any set of values:
$$\text{Let } B \subseteq \mathbb{R} \text{, } \ \ P(X \in B) = \sum_{x \in B \cap S_X}p_X(x)$$
We simply need to sum up the probabilities of $X$ being the individual values in B that are also in the *state space* for $p_X$.

It is also true that $\sum{p_X(x)} = 1$ since the map $X$ must be *complete*.


