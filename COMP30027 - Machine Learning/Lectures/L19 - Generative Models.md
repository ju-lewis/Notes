
**Goal:** model the probability density function of what you want to generate
- Often hard to model the PDF directly

Instead:
- Map to a lower-dimensional "latent space"

Training requires a significant amount of data
- GPT-3: 570GB of text
- Stable diffusion: 2.3 billion images

Training is unsupervised (or self-supervised)
- Doesn't require human labels


Usually, we hide part of the input and ask the model to predict it
- Masked language modelling
- Image denoising (remove Gaussian noise from an image)


# Autoencoders
Essentially, neural networks for unsupervised learning

Hidden layers transform the input to a latent space, then back into the "feature space" on the output.

Hidden layer represents the input in terms of *latent variables*
- In the simplest case, the hidden layer learns PCA

**Variational autoencoders** can perform simple image gen
- Variation -> novel instances

**Advantages**
- Learns small latent representations
**Disadvantages**
- Can be difficult to train complex autoencoders



# Generative Adversarial Networks
Two adversarial networks:
- Generator
- Discriminator

Generator maps noise to an input image
Discriminator is a binary classifier that outputs real/fake


## Generator
Learns a probability distribution
- Tries to map to novel samples

Almost like a CNN in reverse
- Projects a vector (of $x$ random values) into a 2d $y$ channel image
- Performs reverse convolutions and inverse pooling to upscale the image


## Training
If the discriminator is too good:
- Easily rejects all fake inputs
- Not much information to train generator
If the discriminator is too bad:
- Easily confused by fake inputs that don't look real
- Generator will learn a poor solution

It's difficult to find the balance

### Evaluation
- Outputs should look real
- Outputs should not be identical to inputs
	- We can determine this by checking nearest neighbours in the training data
- Outputs should be diverse (avoid *mode collapse*)


### Summary
**Advantages**
- Model, and generate samples from complex probability distributions
**Disadvantages**
- Hard to train
- Can be unstable
- Difficult to evaluate
- May learn incorrect distributions



