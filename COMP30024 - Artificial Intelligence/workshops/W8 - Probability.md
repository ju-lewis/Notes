
# 1. Under Oath
**1a.** 
$P(T=b|O=b)=\frac{P(T=b, O=b)}{P(O=b)}$
$P(T=b|O=b)=\frac{P(O=b|T=b)P(T=b)}{P(O=b)}$
$P(T=b|O=b)=\frac{0.75P(T=b)}{P(O=b)}$


$P(T=g|O=b)=\frac{P(O=g|T=b)P(T=g)}{P(O=b)}$
$P(T=g|O=b)=\frac{0.25P(T=g)}{P(O=b)}$

Hence it is 3x more likely the taxi is blue

**1b.**
Plugging in the values to the above formulae

$P(T=b|O=b)=\frac{0.75 \cdot 0.1}{P(O=b)}$
$P(T=b|O=b)=\frac{0.075}{P(O=b)}$

$P(T=g|O=b) = \frac{0.225}{P(O=b)}$

$\forall P(O=b) \in [0,1], P(T=g|O=b) > P(T=b|O=b)$

Hence it is 3x more likely to be green.


# 2. Counterespionage

G = guest chosen (either Russian or American)
- Note: word detected = guest chosen

L = letter chosen

$P(G=r) = 0.2$

$P(L=l | G=r) = 1/6$
$P(L=l|G=a)=1/4$

We know an L was chosen, hence we want to determine:
$P(G=r|L=l) = \frac{P(L=l|G=r)P(G=r)}{P(L=l)}$
$P(G=r|L=l)=\frac{(1/6) \cdot (1/5)}{0.2(1/6) + 0.8(1/4)}$
$P(G=r|L=l)=\frac{1}{7}$

# 3. Monty Hall

**3a.**

