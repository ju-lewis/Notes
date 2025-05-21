
# 1. Used Cars

**1a.** Pat is more likely to have the better car, due to the larger number of samples increasing the chance of considering a car with higher expected utility

**1b.** Pat is also more likely to be 'disappointed' with the car's quality, as there is a higher likelihood of considering an outlier when considering more samples

# 2.
P(S) = 0.75
P(A) = 0.25

P(round | S) = 0.7
P(red | S) = 0.7

P(square | A) = 0.9
P(brown | A) = 0.9

**2a.**
Network 3 (The flavour is chosen first, which directly influences the probability of the wrapper and colour)

**2b.**
Network 3 is also the best representation

**2c.**
Yes, they're prior probabilities so they have no impact on each other

**2d.**
P(red) = P(red | A)P(A) + P(red | S)P(S)
P(red) = (1-0.9)0.25 + (0.7)0.75
P(red) = 0.55

**2e.**
P(S | round, red) = $\frac{P(round, red | S) P(S)}{P(round, red)}$

P(S | round, red) = $\frac{P(round | S) P(red | S) P(S)}{P(round, red | S) + P(round, red | A)}$

P(S | round, red) = $\frac{0.7 \times 0.7 \times 0.75} {0.7\times0.7\times0.75 + 0.1 \times 0.1 \times 0.25}$

P(S | round, red) = $147/148 = 0.9932$


**2f.**
$U(S) = a$
$U(A)=b$
$V = aP(S) + bP(A)$

**2g.**
If the box is *unopened*, then the value doesn't change (we can't see anything anyway)

# 3.  Textbook Purchase
Let $B$ be an indicator of whether the agent buys the book
Let $M$ be an indicator of whether the student masters the material in the book
Let $P$ be an indicator of whether the student passes the course

Let $U$ be the utility node
- \$-$100$ for buying the book
- \$2000 for passing the course
- \$0 for not passing

**3a.**
B -> P
B -> M
M -> P
B -> U
P -> U

**3b.**
$U(b) = -100 + U(p)P(p|b)$
$U(b)=-100 + 2000\times P(p|b)$
$U(b) = -100 + 2000 \times (P(p|m,b)P(m|b) + P(p|\neg m,b)P(\neg m | b))$
$U(b)=-100 + 2000(0.9 \times 0.9 + 0.5 \times 0.1)$


