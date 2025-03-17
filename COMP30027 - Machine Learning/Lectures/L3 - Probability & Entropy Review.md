
# Attribute / Variable Types

**Nominal** (aka categorical)
- Variable can take multiple values which are discrete types or categories
- There is *no natural ordering*
	- Equally dissimilar from eachother
**Ordinal**
- Variable has discrete values with a natural ordering
- Examples:
	- `beverageSize`: Small, medium, large
	- rating: x/5 stars
Nominal/ordinal distinction can be unclear

**Continuous**
- Variable is real-valued with a defined zero point and *no explicit bound*
	- Distance
	- Time
	- Price

>[!note]
>For practical purposes in machine learning, we typically treat `int` variables as continuous variables.

Attribute types matter because they encode information about the attributes.


# Probability Review

Learning implies uncertainty
- Probability too complex to solve exactly
- Data is ambiguous or incomplete

How do we make smart decisions under uncertainty?

Honestly just check probability notes lol

## ML Definition For Probability Distribution

"A list of all possible outcomes of a random variable, along with their probability values, or a mathematical function that describes possibilities of each outcome"

**Multinomial Distribution**
More general case of binomial
$$P(X_1=x_1, X_2=x_2,...,X_n=x_n) = (\sum^{n}_{i=1}x_i)!\prod_{i=1}^{n}\frac{p_i^{x_i}}{x_i!}$$ 
## Probability Models
A probability model is a mathematical representation of a random event

It consists of:
- A sample space
- Events
- A probability distribution of the events

The model predicts the relative frequency of each event x: P(x)


# Entropy

Measure of information
- How much information is available for learning?

Shannon Entropy is a measure of unpredictability, the information required to predict an event
- Measured in *bits* (*b*inary dig*its*)

$$H(X) = -\sum_{i=1}^{n}P(x_i)\log_2P(x_i)$$
Define $0\log_20 = 0$

Lower entropy implies higher predictability
For a system with $N$ outcomes, entropy range is $0 \text{ to } \log(N)$ 

Higher entropy also suggests there is more embedded information
- For ML typically low entropy is helpful because the system is more predictable
- For sensors/reading information high entropy is good because it implies more can be learned from observations

![[entropy.png]]



