
# Representational Learning


## Text Representation
How to represent the "main idea" of a text?

Simple option: **Bag of words**
- Ignore order
- Form simple count vectors
- Works quite well for many tasks
- *Problems:*
	- Missing context
	- Order
	- Understanding of synonyms and phrases
	- Curse of dimensionality


## Image Representation
How to represent the "main idea" of an image?

Images are made up of pixel values, each pixel has an RGB value
- How much information can you get from "bags of pixels"?
Pixel level representations can work for constrained tasks

More complex visual tasks require more complex features (shapes, objects)
- Curse of dimensionality also remains

## Representation Leaning in NNs

Networks lean a feature hierarchy - from simple combinations to more complex features (embeddings)


# Neural Network Overview
Neural networks are inspired by the biological principle of Hebbian learning
- If activation from dendrites exceeds a threshold, the axon is 'activated'


The basic unit of a neural network is the neuron:
- Input vector
- Output scalar
- Activation function hyperparameter
- Parameters (weights)

## Perceptron
Neural network with just a single neuron
- Binary linear classifier

Common activation functions:
- Sigmoid function
- Hyperbolic tan
- Rectified linear unit (ReLU)
### Training
**Goal**: Minimise error through updating weights

- Each iteration over the whole dataset is called an epoch

Perceptron training algorithm:
```
repeat
	for each training instance (x, y_i) do
		compute y_hat = f(w(x_i) + b)
		for each weight w_j do
			w_j <- w_j + a(y_i - y_hat_i)x_ij
		end for
	end for
until stopping condition is met
```

### Properties
- Guaranteed to converge for linearly separable data, but the convergence point depends on hyperparameter selection
- Not guaranteed to maximise margin between classes
- Not guaranteed to converge over non-linearly separable data


>[!Note]
>A perceptron with a sigmoid activation function (plus a binary step to convert the output to 0 or 1) is equivalent to logistic regression


A logical extension of the perceptron is extending the model to multiple outputs.
- Each 'parallel stack' of perceptrons is considered a layer

## Multilayer Perceptrons

MLPs are characterised by having at least 1 hidden layer

### Hidden Layer
Choosing the number of hidden layer neurons depends on factors like complexity of decision boundaries
- In practice it's common to pick an arbitrary value between input and output size
	- This is definitely not a rule thought


#### Training
There is not just one "correct" output for the neurons in a hidden layer
- We use stochastic gradient descent with backpropagation

Look at the partial derivatives of error with respect to each weight
- Update in the direction that would reduce error
- Propagate errors back to each of the earlier layers


### Output Layer
- Structure depends on task
Common options:
- Binary classification
	- 1 output neuron with a simple activation function
- N-way classification
	- N output neurons with *softmax*
- Regression
	- 1 output neuron with identity activation function


### Properties
- Universal approximation theorem
	- Can approximate any function in $\mathbb{R}^n$
- Therefor the network can learn *any* decision boundary

**Advantages**
- Can be adapted to many problems
- Universal approximator
- Representation learning in hidden layers
**Disadvantages**
- Very high number of parameters
	- Slow to train
- Prone to overfitting
- High memory requirements




