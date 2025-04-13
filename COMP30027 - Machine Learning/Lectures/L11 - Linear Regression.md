
# The Regression Problem
What if the **concept** is continuous?

Continuous attributes -> Continuous concept

## Linear Regression
At its most basic, the relationship between continuous attributes and a concept can be expressed as a *hyperplane*

$$c = w_o + \sum_{k=1}^Dw_ka_k$$
$$c = \vec w \cdot \vec a$$

Linear regression makes the assumption that the relationship is linear!
- This assumption is not always true, but does significantly simplify the search space
- For *some* variables, this assumption makes sense
	- It's very common to observe some degree of monotonicity

### Training and Prediction
Training set: $N$ examples
- $(\vec{x_1}, y_1), (\vec{x_2}, y_2), ..., (\vec{x_N}, y_N)$

Find the optimal $\vec{\beta} = [\beta_0, \beta_1, \beta_2, ..., \beta_D]$

Predict a continuous valued output $\hat{y} = \vec{\beta}\cdot \vec{x}_{\text{test}}$


### Fitting the Model
We want to choose the *best line*
- Operationally, the line that minimises the distance between all points and the line

**Least squares method**
- Find the line that minimises the sum of squares of vertical distance between predicted $\hat{y}$ and actual $y$.

Minimise the (Mean Squared Error) *MSE*  of $N$ data points

$$\vec{\beta} = \arg_\beta{\min{\text{MSE}}}$$

# Parameter Estimation

Given an evaluation metric $M$ (like accuracy or error), a dataset $T$ (consisting of attributes $X$ and labels $y$), and a learner $L$ with parameters $\theta$

if $M$ is error rate,
$$\hat{\theta}=\arg\min_{\theta \in \Theta}{\text{Error}(\theta; L, T)}$$

## Computing the Optimal Solution


### Analytic Solution
Closed form, can be computed exactly

Requires solving partial derivatives with respect to all attributes
$$\frac{\partial(\text{Error})}{\partial \theta_1}=0, \text{etc...}$$

For linear regression:
$$\hat{\theta} = (X^TX)^{-1}X^T\vec{y}$$
Derivatives can be undefined or unknown (or incredibly expensive to compute)

MSE is a convex function, so the local minimum is a *global* minimum

### Grid Search (Exhaustive Solution)

For each $\theta \in \{k_1, k_2, ..., k_n\}$ calculate the error and choose the values that minimises the error

Works for methods with a small number of hyperparameters


**Grid search** is the continuous analogue of exhaustive search
- Divide the attribute ranges into equal-width samples and compute error for each sample


### Iterative Optimisation

**Standard Steps**
1. Initialisation
2. Evaluate
3. Terminate (decide whether to stop)
4. Update
5. Repeat

## Gradient Descent
$$\theta^{\text{iter}+1}:=\theta^{\text{iter}}-\alpha \nabla Error(\theta^{\text{iter}}; L, T)$$
Each update slightly reduces error

**Choosing a good $\alpha$ is very important**



# Evaluation and Extension

**Mean Square Error (MSE)**

**Root Mean Squared Error (RMSE)**

**Root Relative Squared Error (RRSE)**
- Relative to baseline $\bar{y} = \frac{1}{N}\sum y_i$

**Correlation Coefficient**


Which metric to use?
- Need to consider what the metrics actually measure


