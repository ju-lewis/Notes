

# 1. Noughts and Crosses

**1a.** State space size approximation

Number of possible arrangements of pieces in general = ${9}\choose{n}$
Number of possible 'colourings' of the arranged pieces = ${n}\choose{\lfloor n/2 \rfloor}$

Hence, the number of possible states with $n$ pieces is: ${{9}\choose{n}}  {{n}\choose{\lfloor n/2 \rfloor}}$

So the full state space size is:
$$\sum_{n=0}^9{{{9}\choose{n}}  {{n}\choose{\lfloor n/2 \rfloor}}} = 6046$$


**1b.**
i. $f(s) = 3(0)+3-(3(0)+0) = 3$
ii. $f(s) = 3(2)+0-(0(1)+1) = 6-1 = 5$
iii. $f(s) = 3(0) + 0 - (3(1) + 0) = 0-3 = -3$


**1c.**


# 2. Great Expectations
The real world likely has an element of non-determinism, i.e. it is a stochastic environment

# 3. Suboptimal
The minimax algorithm will perform *no worse* than if the opponent is optimal, however it could be better if it is known that the opponent isn't playing optimally

# 4. Optimal Ordering
