
## Machine Learning Methodology

**ML Method**
- Training
- Testing
- Run-time Application


### Neuron Structure

Input function
- Weighted sum
	- Dot product between weights and inputs
- Activation function
	- Linear
	- Step
	- ReLU
	- Sigmoid
- Output

Layers of neurons are interconnected
- Multi-layered perceptron

#### Network Architectures

Feedforward
- Signal simply passes sequentially through layers
Recursive
- Signal can loop back and reinforce *itself*
Recurrent
- Signal can 'see' repeating input
Convolutional
- Small local input groups can be treated together
	- Pooling layers


#### Training via Back-propagation
Initially randomise all weights, update weights using partial derivatives with loss function.

### Embeddings

**Encoding text**

We know text can be represented as a bag of words, but *words can also be represented as a bag of words* by considering words that frequently co-occur with the given word

- Bag of words
- tf.idf
- We can use a neural network to compute even better counts (*embeddings*)
	- Initialise each word as a random vector of words
	- Train the NN with many sentences anchored on each target word
	- Use backpropagation to adjust each vector's values
	- Words with related meanings will end up with similar vector score distributions


## Language Models


### Building a Language Model
1. Scrape text (to construct corpus)
2. Preprocess text, keep punctuation but lemmatize words
3. Move a 'window' of $n$ words across the texts
4. Record every ngram window, counting number of occurrences
	1. e.g. "The White House" may occur lots (word 3-gram)
5. Normalise counts
6. Use logs of normalised counts (they'll be very small)





