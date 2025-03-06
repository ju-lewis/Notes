
## Linear regression

Predict the value of a dependent variable (Y) based on 1 or more independent variables (X)

### Simple Linear Regression Model
- Only one independent feature X
- We are trying to predict Y
- Relationship between X and Y is a linear function

*Assumed causality*
- Changes in Y are assumed to be caused by changes in X


$$Y_i = \beta_0 + \beta_1X_i + \epsilon_i$$
$Y_i$ is the dependent variable (what we're predicting)
$\beta_0$ is the intercept 
$\beta_1$ is the slope coefficient
$\epsilon_i$ is the error term


#### Least Squares Errors
We obtain $\beta_0$ and $\beta_1$ by finding the values that minimise the sum of squared differences between truth values and predicted values.
$$min\sum(Y_i - \hat Y_i)^2 = min \sum(Y_i-(\beta_0 + \beta_1 X_i))^2$$


#### Interpolation vs Extrapolation
You can only assume the observed linear relationship holds within a reasonably small range of the training values.


### Multiple Regression

A researcher may be interested in predicting more than 1 dependent variable

Same thing, but we have more equations to describe each dependent variable.




**Supervised vs Unsupervised Learning**

Supervised -> Labelled data, we can predict labels or compare values
Unsupervised -> Unlabelled data, tasks like clustering, dimensionality reduction



### The Generalisation Challenge

Overfitting occurs when the model 'memorises' the training data
- Generalises terribly
- Bias/variance error

**Evaluation methods - training and test sets**

Divide total dataset into training and test sets


**Cross Validation**
Split dataset 90-10 train-test
- Repeat 9 more times, with different 10% for test set each time


