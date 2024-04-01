

# Autoregressive generation
---
_Predict a sequence of tokens, one token at a time_

*  Starts from a _start token_ and generates until it generates a _stop token_
* Context (input tokens) are all the words before the current token
* ![[Pasted image 20240329170110.png|350]]



# Searching for most probable sequence
---

* Casual language models are trained to estimate the probability of a sequence of tokens:
* ![[Pasted image 20240329170539.png|350]]
* How to predict the most probable output? Way to expensive with a big vocabulary


## Greedy Search
_Choose the most likely token every time, without considering future options_

* Very fast and simple to implement
* Usually not a large performance drop with a good model
* Like a beam search where $k=1$

## Beam Search
_Algorithm for estimating most probable sequence, prunes future tokens_

* Most popular search method, drops the complexity substantially
* Choose a beam size $k$ (for example $k=2$)
* Only take the $k$ most probable candidates seen so far into account
* When moving forward to predict the best token, greedily choose the beam size number of most probable tokens. 
* Complexity drops from $O(|V|^{t})$ to $O(k\cdot t)$
*  In practice, beam/greedy search can lead to outputs with infinitely repeated n-grams

	![[Pasted image 20240329173419.png|350]]
	![[Pasted image 20240329173733.png|350]]



# Random Sampling
---
_Introduce randomness when choosing the next token_

* *Natural language does not maximize probability* - Holtzman et al., 2020"
* Humans don't always pick the 'optimal' words, therefore a 'perfect' sequence of words might sound unnatural


## Sampling vs Beam Search

* Outputs from beam/greedy search can sound stiff, generic, repetitive or simply boring
* That's exactly what we want from machine translation (most of the time), to exactly translate the source text without any creative variation.
* Not great for chatbots, for example
	* We want them to get 'creative'
* In practice, beam/greedy search can lead to outputs with infinitely repeated n-grams


## Random Sampling
_Introduce randomness when choosing the next token_

* Randomly pick a token from the conditional distribution $P(W_{i}|W_{0:i-1})$
* In practice all the three below are often used at the same time
* The quality of the generated text is highly dependent on these hyper-parameters
* Degenerate outputs are still an issue and better decoding strategies are an active research area

### Temperature
* We can control the amount of "randomness" (entropy) with the **temperature** hyper parameter $T$
* When $T\rightarrow0$, we get greedy search; when $T\rightarrow \infty$, we sample uniformly
* When unlucky, this method can sample even the least probable token. Can be prevented with **top-k sampling** or **top-p (nucleus) sampling**
* $p_{i}=\dfrac{e^{\dfrac{x_{i}}{T}}}{\sum_{j}{\frac{e^{x_{j}}}{T}}}$
* ![[Pasted image 20240329221130.png|350]]

### Top-k sampling
_Select the k most probable tokens and sample from those_
* Can be used to control precision vs creativity
* Doesn't take the probability distribution into account, one very likely tokens vs hundreds of equally likely tokens
* Introduced by Fan et al., 2018

### Top-p (nucleus) sampling
_Sample smallest set of tokens whose sum of probabilities exceeds p_
* Set of sampled tokens dynamically changes according to the probability distribution
* Introduced by Holtzman et al., 2020


