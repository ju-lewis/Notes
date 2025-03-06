# Algorithms
- Naive Bayes Classifiers
- Decision trees
- Support Vector Machines
- Linear Regression
- Logistic Regression
- Gaussian Mixture Models
- Hidden Markov Models
- Perceptrons
- Deep Neural Networks

---
# Terminology
- **Instances** - Input to the model
	- Also called *exemplars* or *observations*
- **Attributes** - Measured aspects of each instance
	- Also called *features*
- **Concepts** - Things we aim to learn
	- Often in the form of *labels*

## Concept Examples
- Discrete class labels (classification)
- Numeric output (regression)
- Clusters
- Probability of an event
- The most likely order of an event
- A sequence of commands
- A complex model

---
# Supervised vs. Unsupervised

*Supervised* methods receive labelled instances during training, learn the associations between attributes and concepts

*Unsupervised* methods received unlabelled data and learn from attributes only
- Discover dataset structures
- Discover *latent variables* that explain patterns in the observed instances
- *Reduce dimensionality* for a supervised learner


### Supervised Train and Test
Goal: Learn mapping from attributes to concepts
**Training**: Model sees many examples of attributes-concept pairs
**Test**: Model sees a new set of attributes, predicts concepts
**Evaluation**: 


### Unsupervised Train and Test

Goal: Learn mapping from attributes to concepts

**Training**: Model sees many examples of attributes
**Test**: Model sees a new set of attributes, predicts concepts
**Evaluation**: ?
- For probability models, we can see if future samples from the same distribution are well predicted by the model


## Association Learning
Detect useful patterns, associations, correlations, or causal relations

---

# Levels of Analysis

## Marr's Levels of Analysis
A framework for understanding information-processing systems

**Computational level**
- What's the goal of this system?
- What structure does this machine learning model expect to see in the world?
- What rule/pattern/model/etc. explains the data?

**Algorithmic level**
- How do you achieve the goal?
- Algorithms and data structures
- Given a model, fit the parameters to the data
- Usually this involves minimising a cost/loss function

**Implementational level**
- Physical implementation (circuits, neurons)
- How to find that best fit in finite time?
- Not always possible to solve exactly



>[!example] Example: Linear Regression
>
>**Computational**: The goal is to minimise error using a fitted linear function
>**Algorithmic**: Least-squares optimisation
>**Implementation**: Linear algebra or gradient descent (we can directly solve linear regression)

### Model Inaccuracies
What went wrong at the *computational*, *algorithmic*, and *implementation* levels?

Example:
- Did we have the wrong assumptions?
- Did we pick the wrong models?
- Did we use bad loss metrics?


