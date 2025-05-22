
Labelling data is often the bottleneck for machine learning
- Switchboard corpus: 400 hours of annotation time per hour of speech data
- Image labelling: often 30-60 minutes per image for a complete segmentation

# Data Augmentation

**Bootstrap Sampling**
- Create "new" datasets by resampling exisiting data, with or without replacement
- Common in neutral network trainig (mini-batch)
- Each batch has a slightly different distribution

**Data Manipulation**
- Another option: add a small amount of noise to each instance to create multiple variations
- These perturbations should not change the instance's label
- Generally they should be similar to real world variation

**Data Synthesis**
Create artificial data using another machine learning method
- Train a probability distribution on labelled data
- Sample the probability distribution to produce new instances
	- GAN, variational autoencoders, etc.

## Advantages
- More data almost always improves performance
## Disadvantages
- Biased training data
- May introduce fake features
- May propagate errors
- Increases problems with interpretability

# Semi-Supervised Learning
Semi-supervise learning is from both labelled and unlabelled data

## Self-Training
Assume you have labelled data and unlabelled data
Repeat:
- Train model on labeled
- Apply predictions to unlabelled
- Choose high confidence predictions to incorporate into the next iteration training set

Propagating labels requires some assumptions:
- Points that are nearby are likely to have the same label

## Active Learning
An active learner "poses queries" to annotators

Query strategies:

*Alternatively:
- margin sampling selects queries where the classifier is least able to distinguish between two categories
- Or better yet, use entropy as the measure


*Query by Committee (QBC)*
- Select instances with highest disagreement between classifiers
- Send these to annotators

### Advantages
- Robust
### Disadvantages
- Difficult to justify
- Introduces bias
- Sensitive to label noise

# Data Considerations
Does the training data accurately reflect the real world?:
- Tendency to use data that is convenient

>[!Example]
>Performance in object classification is surprisingly linked to geography

## Dataset Bias
What happens when some groups are less represented than others in a dataset?
- Less contribution to loss function
- Poorer model fit in this group
- Poorer generalisation to ew examples of this group due to lack of training diversity

### Recommendations
- Check your dataset for biases
- Be aware that datasets may be biased in ways you haven't thought of
- The fact that something is on the internet doesn't mean you can use it to train AI


