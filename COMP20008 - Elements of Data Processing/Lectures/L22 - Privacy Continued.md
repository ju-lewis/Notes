
## Differential Privacy

Some queries are often more intrusive than others

We want to modify the privacy ad-hoc (query-by-query) basis:
- Provide results



### Local vs Global Differential Privacy

#### Local:
- Each person is responsible for adding noise to their own data
	- They 'flip a coin' in secret and give a set answer (not necessarily true) if it comes up heads, and tell the truth if it comes up tails

>[!example]
>Question: Do you use drugs?

*Issue:* local privacy requires knowing who else is in the data/survey



#### Global/Centralised Privacy

Noise is added by the DB owner

![[global-privacy.png]]


*Adding different amounts of noise*:
Generate random values with a distribution with mean 0
- Standard deviation is 1/(privacy loss budget)

This prevents characterising data from being obtained from a single query
- But the data is still accurate as it still averages out to the true value



## Another Approach to Noise
Instead of modifying the values, we can *withhold* data records

**How many records should we drop?**
- Drop as few as possible -> maintain data
- Privacy loss budget $k$
	- Integer expressing 'how private' the results should be
	- How many records can we withhold before data is no longer useful
We need to strike a balance between privacy and accuracy

$k$=0 implies we don't do anything - since we can't afford to lose any information


**What records should we drop?**
- Global sensitivity $G$
	- Number expressing how much different the inclusion or absence of an *individual record* could make to the result




### Determining $k$

>[!note]
>The probability that the noisy released result will be $R$ must be nearly the same regardless of an individual's participation
>
>$A$ = Probability result is $R$
>$B$ = Probability result is $R$
>
>Choose $k$ to guarantee:
>$A \leq 2^k \times B$
>
![[privacy-budget.png]]


### Determining $G$

....



### Putting $k$ and $G$ Together
We want to drop as little data as possible within our privacy loss budget ($k$)
- And we want to target the 'most damaging data' (based on $G$)


>[!summary]
>Differential privacy guarantees that the ...



## Ethics - Continued

### EU's Digital Service Act (2024)
- Protects users against manipulative algorithms that *promote hate speech, etc.*

### Digital Market Act
- Identifying gatekeepers (controllers of digital technologies)
- Enforcing gatekeepers to comply with new prohibitions/obligations

### EU AI Act


### United States Generative AI Copyright Disclosure Act
- Requires Gen AI creators to disclose information sources

### Ensuring Likeness Voice and Image Security (ELVIS) Act
- Protects artists and songwriters likeness



Australia has 8 AI Ethics Principles
- Governed by existing legislation



## What is Ethical Action?

We need to think about whether analysing data in a specific way or sharing (even public) data impacts people's lives
- How could findings be used by an adversary? 


