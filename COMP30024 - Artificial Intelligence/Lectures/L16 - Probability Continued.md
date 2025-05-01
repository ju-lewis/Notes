
We can determine the probability of any propositions by enumerating across the joint distribution table

## Inference by Enumeration

Typically, we're interested in the *posterior joint distribution* of the *query variables* $Y$ given specific values $e$ for the *evidence variables* $E$.

Let the *hidden variables* be $H = X-Y-E$

Then, the required summation of joint entries is done by summing out the hidden variables:
$$P(Y|E=e)=\alpha P(Y,E=e) = \alpha \sum_{h}P(Y,E=e,H=h)$$

The terms in the summation of the joint entries because $Y$, $E$, and $H$ together exhaust the set of random variables

*Obvious problems*:
- Worst case time complexity $O(d^n)$ where $d$ is the largest arity
- Space complexity $O(d^n)$ to store joint distribution
- How to find the numbers for $d^n$ entries?


### Independence

Absolute independence is powerful but rare

### Conditional Independence

>[!Example]
>If I have a cavity, the probability that the probe catches it is not dependent on whether I have a toothache
>
>$$P(\text{catch|toothache,cavity})=P(\text{catch|cavity})$$
>
>Catch is conditionally independent to toothache, given cavity.
>
>We can use this to decompose with the chain rule:
>$P(\text{toothache, catch, cavity})$
>$= P(\text{toothache|cavity,catch})P(\text{catch|cavity})P(\text{cavity})$
>$= P(\text{toothache|cavity})P(\text{catch|cavity})P(\text{cavity})$
>
>We make this second simplification step because of catch being independent to toothache given we have a cavity.

This is how *Naive Bayes* models work!
- Assume independence of all effects (observable attributes)


# Summary
- Joint probability tells us probability of every atomic event
- Conditional independence allows us to simplify non-trivial domains