
Regression and classification are technically interchangeable
- It just depends on where you perform discretisation


>[!Note] Logistic Regression Strategy
>Attempt to model $P(c|\vec{x})$ directly - we'll fit a continuous function for $P(c|\vec{x})$ that lets us classify instances

Assuming a 2-class problem (Y/N)
- $P(c = Y|\vec{x})$: probability of an instance with class $Y$

### Deriving the Modelling Function
How should we map the class probabilities to a continuous function?
- Logistic regression -> logistic function


**Option 1 - Linear Function**
This is the most simple method, but not optimal
$P(c=Y|\vec{x})=\vec{\beta} \cdot \vec{x}$
- Fit $\vec\beta$ to optimise error metric
*Drawbacks*:
- No guarantee $\hat P \in [0,1]$
	- We can't limit domain, because then we couldn't classify all instances
- Meaning of probabilities outside $[0,1]$ is unclear

**Option 2 - Exponential Function**
$P(c|\vec{x})=e^{\vec \beta \cdot \vec x}$

*Drawbacks*:
- Curve is unbalanced
	- Fine-grained near 0, coarse near 1


**Option 3 - Logistic (Sigmoid) Function**
We want the same response behaviour for high and low $P$

$\text{logit}P(c|\vec{x}) = \log \frac{P(c|\vec{x})}{1-P(c|\vec{x})}$

$$P(c|\vec{x})=\text{logistic}(\vec \beta \cdot \vec x)=\frac{1}{1+e^{-\vec \beta \cdot \vec x}}$$


## Parameter Estimation

How do we determine $\vec\beta$?
- We need to define an objective function to optimise the parameter

We can use gradient descent here

Given $N$ independent training instances $(\vec{X}, Y)$, we want to choose $\vec \beta$ to maximise the likelihood of observing them
$$P(Y|\vec X, \vec \beta) = \prod_{i=1}^{N}P(y_i|\vec{x_i}, \vec \beta)$$
$$\hat \beta = \arg \max_\beta \prod_{i=1}^N(h_\beta(\vec{x_i}))^{y_i}(1-h_\beta(\vec{x_i}))^{1-y_i}$$

## Multi-class Classification
Multinomial logistic regression
- Take one class as **pivot**
- For every other class $c_j$, build a regression model
- Treat $c_j$ as class $Y$ and the pivot class as $N$
- End up with $|C| - 1$ logistic regression models
- Predict the class according to the one with the highest probability score



