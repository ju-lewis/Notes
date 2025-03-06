
## Vector space of text

Once we normalise and vectorise our document (usually with TF.IDF scores), we can compare document similarity through distance computation.

### Manhattan Distance
(Also known as City Block distance)

$$\text{Manhattan}((x_1, y_1), (x_2, y_2)) = |(x_2-x_1)| + |(y_2-y_1)|$$


### Euclidean Distance
$$\text{Euclidean}((x_1, y_1),(x_2, y_2)) = \sqrt{(x_2-x_2)^2+(y_2-y_1)^2}$$


### Minkowski Distance
The general 'normal' distance for all dimensions

$$\text{Minkowski}(u,v)=(\sum_{i=1}^{n}|u_i-v_i|^p)^{(\frac{1}{p})}$$

Where $u$, $v$ are vectors in the $p$-dimensional vector space

Properties of Minkowski Distance:
1. Nonnegative
2. Identity (d(x, y) = 0 if and only if x == y)
3. Symmetry
4. Triangle Inequality


Remember these distance metrics only make sense for normalized word counts!

 This is where **cosine** similarity comes in handy.

### Cosine Similarity

Cosine similarity compares the vectors by their angular distance, instead of scalar distance.

In general,

$$\text{Cosine similarity}(\vec u, \vec v) = \frac{\vec u \cdot \vec v}{|\vec u||\vec v|}$$
### Dice Similarity
$$\text{Dice similarity}(\vec u, \vec v)=\frac{2|\vec u| |\vec v|}{|\vec u|+|\vec v|}$$
### Jaccard Similarity
Jaccard is used when you consider data points (words) as sets.
$$\text{Jaccard Similarity}(A, B) = \frac{A \cap B}{A \cup B}$$


## What is Document Distance used for?
1. Retrieval
2. Duplicate checking
3. Clustering
4. Topic modelling
5. Trend analysis


## Visualisation 
Visualisation allows us to see what clustering/patterns occur
The human eyes/brain are powerful for detecting structures


Data driven hypothesis generation - contrast to formal hypothesis testing
- Data-driven is 'bottom-up': the data -> you
- Hypothesis testing is 'top-down': your mind -> the data


*Exploratory data analysis doesn't begin with a hypothesis.*


### What is a distribution?
The values of a quantitative variable have a range (e.g. percentage being between 0 and 100)

The set of data points in the range is a *distribution*

Measures of location:
- Mean
- Median
- Mode
- Min/Max
- Quartile, Percentile
- Variance / Standard deviation
- Range
- Interquartile range: Q3 - Q1
- Skewness - does the distribution have a long tail?


We can obtain all of the information using `pandas`:
```python
import pandas as pd

pd.DataFrame.describe()
```


### Univariate data visualisation
- **Histograms**
	- Range
	- Central location (left or right skewed/tailed?) tail side -> skewed side
	- Symmetry
	- Modality (how many peaks?)
	- Outliers
- **Binning**
	- We need to work out the best 'resolution' (number of bins) for our histogram
	- ![[binning.png]]
	- Too many bins -> many empty bins
	- Too few bins -> outliers in frequent bins
- **Boxplots**
	- ![[boxplot.png]]


### Multivariate data visualisation
- **Scatter Plot**
	- Can perform regression (lines/curves of best fit)
	- Correlation
		- Direction
		- Strength
	- When there are *too many* data points, we can fix this by:
		- Sampling
		- Jittering (adding uniform random noise)
		- Use other kinds of plots
- **Contour Plots**
	- Introduce a 3rd variable indicating *data density*


For more than 3 dimensions we can add additional 'info carriers':
- Colour
- Size
- Shape
- etc.



