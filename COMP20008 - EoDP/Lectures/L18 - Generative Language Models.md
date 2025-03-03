

## What Makes an LLM *generative*?

So far our LLMs are 'passive' they can simply associate tokens in embedding space.
- You need to provide information in a very specific format

OpenAI developed a method to make them generative - simple English input and English output.


## N-Gram Language Models

### Left-to-Right Generation
#### Output Generator Loops

1. Input some text (the prompt)
2. Use it to select possible response ngrams (by matching the prompt's microfeatures) 
3. Pick a matching ngram 
4. Output it
5. Append it to the prompt and repeat
6. Continue until some threshold is reached


It took an extremely long time before GenLLMs could generate coherent outputs
- Just connecting overlapping token ngrams doesn't guarantee grammaticality!

It's also difficult to know when to stop.


**Detriments of this technique**:
- Near-distance falseness (hallucination)
- Long-distance incoherence
- Socially unacceptable output


OpenAI used a significant amount of reinforcement learning from human responses.



A significant amount of current research is looking at:
- Smaller models
- Private LLMs
- *RAG* (adding your own content without training)
	- Retrieval augmented generation
- *Agency* Adding functionality not native to LLMs
- Explanation: Describing what the LLM did
- Hardware acceleration


>[!tldr] Summary
>We now have a very big 'database' of text fragments and a chat loop that allows the model to predict n-grams based on a prompt.


## Agency
How to make LLMs able to act in the world?

Need to build interface channels that connect LLM output to word system software



## Images and Videos

Just like 'text ngram microfeatures', create 'image microfeatures' that are associated with words

Start with a random field of coloured dots

To make an image given prompt words
1. Find matching microfeatures
	1. These provide incipient portions of images
2. Match them into the random dot field where they best fit
3. Unify them to create new/stronger microfeature regions
4. Repeat, gradually growing the local contexts by merging in the most appropriate microfeature snippets for an increasingly specific picture


### Image Interpretation Error
*NN microfeatures are not the same as the features people see!*

We can use an adversarial approach to train image creation NNs to make images that look similar to NNs but look very different to humans



