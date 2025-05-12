
## Deep Learning Overview

Deep learning refers to neural networks with a large number of hidden layers
- Network depth = number of layers
- Network width = number of neurons per layer

Focus on *representation learning*
- Transformation of raw inputs into a latent intermediate representation

Deep learning started developing around the introduction of GPUs (and the CUDA platform)
- The internet was also crucial in developing training datasets
- e.g. ImageNet


## Convolutional Neural Networks


Convolutions are defined by:
- *Kernel*: Size of the convolution filters
- *Stride*: How far the window moves at each step

Each convolutional layer learns a hierarchy of image features
- Early layers learn simple features like lines and edges
- Intermediate layers learn relatively simple shapes
- Later layers learn complex shapes similar to the instance class concepts


*Advantages* of convolutional layers:
- Eficient
- Preserve spatial relations

*Disadvantages*:
- Limited kernel size means model is limited to learning local features
	- Mitigated by pooling layers

### Dropout

Randomly discard some neurons (set output = 0)
- Form or regularisation - forces neurons to find useful features independent of each other

### Training

*Loss function*: Cross-entropy loss

$$E = -\frac{1}{N}\sum_{y_i}{log_2(y_i)}$$

We perform batched training to make it feasible to train on massive datasets

### Regularisation
CNNs are prone to overfitting, even on large datasets

Common options:
- L1, L2 regularisation
- Dropout

CNNs are extremely sensitive to some kinds of noise

