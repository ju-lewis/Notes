
# Introduction

Until now, we've considered each instance independently, but in many tasks, there is "structure" between instances

**Sequential Structure**
- Time series analysis, speech recognition, genomic data

**Hierarchical Structure**
- Classifying web pages within a website

**Graph Structure**
- Deriving an influence matrix for a social network

This calls for *structured classification* models which are able to capture interaction between instances

## Markov Chains
A Markov chain describes a system that transits from one state to another based on probabilistic rules
- States
- Initial State Distribution
- Transition

See: [[Week 12 Summary#Computing Markov Transition Probabilities|Probability: Markov Chains]]

**Assumptions**:
- For a sequence of states $q_1, q_2,..., q_T$ at steps $t=1,2,...,T$
- A state $q_n$ is only dependent on state $q_{n-1}$

# Hidden Markov Models

We can see a sequence of observations, but the sequence of states is hidden.

Hidden Markov models (HMM): $\mu - (A,B,\Pi)$
- States: a set $S = \{s_i\}$ with $|S|$ unique values
- Observations: $Y = \{s_i\}$ with $|Y|$ unique values
- Initial state distribution: $\Pi \text{ where } \sum_{\pi_{i}\in\Pi}\pi_i = 1$
- Transition probability matrix: $A = \{a_{ij}\} \text{ where } \sum_{j}a_{ij} = 1 \ \forall \ i$
- Output probability matrix: $B = \{b_{ij}\} \text{ where } \sum_{k}b_{ik} = 1 \ \forall \ i$

HMMs make two independence assumptions
- Observations are only dependent on the current state
- The current state only depends on the immediately preceding model

Essentially the same as regular time-discrete Markov chains from probability, but with an added factor of having a random observation possible at each state

## Evaluation
**Estimate the likelihood of an observation sequence**
- Given an HMM $\mu$ and an observation sequence $\Omega$ determine the likelihood $P(\Omega|\mu)$

- If we know the hidden state sequence (*e.g. hot, hot, cold* for weather) it's easy to calculate: $O(T)$
- If we don't know, then it's much harder to compute: $O(TN^T)$

The probability of the state sequence:
$P(Q|\mu)=\pi_{q_1}a_{q_1q_2}a_{q_2q_3}...a_{q_{T-1}q_T}$

Probability of observing sequence $\Omega$ for state sequence $Q$:
$$P(\Omega|Q,\mu)=\prod_{t=1}^{T}{P(o_t|q_t,\mu)}$$
### The Forward Algorithm
Efficient computation of total probability $P(\Omega|\mu)$ through dynamic programming

Probability of the first $t$ observations is that same for all possible $t+1$ length sequences

Define forward probability as the probability of the partial observation sequence $o_1, o_2,...,o_t$ and state $s_i$ at time $t$ given model $\mu$

By caching forward probabilities we can avoid redundant calculations

**Initialisation**: $\alpha_{1}(i) = \pi_ib_i(o_1)$ (Remember $b_i(o_j)$ is the probability of observing $o_j$ given state $i$)
- Essentially computes the joint probabilities: "What is the probability of observing this outcome *with* this hidden state?"
**Induction**: Computing and memoizing subsequent partial observation sequence probabilities
- "Given all of the previous partial observation sequences, what is the probability of transitioning to state $i$ and observing this outcome?"
	- Compute this for all states for the current observation
**Termination**: Sum all of the values at the final time step; $P(\Omega|\mu)=\sum_{i=1}^{N}\alpha_T(i)$
- This is essentially fulfilling the law of total probability:
	- "The probability of observing the current outcome (and all previous observations) given we've transitioned to state $i$ is $\alpha_T(i)$"
	- Summing across the conditionals yields the final probability



## Decoding
**Find the most probable state sequence for an observation sequence**

>[!Example]
>Given the observation 3-solos, 3-solos, 1-solo (as in purchases of the drink from a store) given the states describe whether the day is hot, or cold. What is the most probable weather sequence?

One method:
- Brute force approach - enumerate the probabilities of all hidden state sequences and sort $O(TN^T + N^T\log N^T)$

A more efficient algorithm is the *Viterbi Algorithm*

### Viterbi Algorithm
Preliminaries: define some variables
- The maximum probability for a partial sequence along a single path
- $\delta_t(i)=\max_{q_1,q_2,...,q_{t-1}}P(q_1,q_2,...,q_{t-1},o_1,o_2,...,o_t,q_t=s_i|\mu)$
- Keep track of the path: for the most probable partial sequence, the hidden state at $t-1$ is $\psi_{t}(i)$

**Initialisation**: $t=1$, state $i=1,...,N$
- $\delta_1(i)=\pi_ib_i(o_1)$
- $\psi_1(i)=0$

**Induction**: $t=1,...,T-1$, state $i=1,...,N$
- $\delta_{t+1}(i) =$
- $\psi_{t+1}(i) =$

For each state at each time step, we store the most probable previous state ($\psi_{t}(i)$)

Once induction is complete (**termination**), we backtrack over the most probable path.

## Learning HMMs
**Estimate parameters of HMM**


### Supervised Case:
Assume we have labelled data, it is possible to use simple Maximum Likelihood Estimation (MLE) to learn the parameters of our model

No state labels?
- Use forward-backward algorithm


# HMM Summary
- HMM is a highly efficient approach to structured classification
- Limited representation of context
- HMM tends to suffer from floating point underflow
	- Use scaling coefficients for Forward Algorithm
	- Use logs for Viterbi Algorithm
# Applications

We can use it for OCR
- There is typically information encoded into the sequence of letters in English words/sentences

