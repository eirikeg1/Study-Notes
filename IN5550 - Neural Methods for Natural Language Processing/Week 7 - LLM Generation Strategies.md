

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
	![[Pasted image 20240329173419.png|350]]
	![[Pasted image 20240329173733.png|350]]



# Random Sampling
---

* _"Natural language does not maximize probability" - Holtzman et al., 2020"
* Humans don't always pick the 'optimal' words, therefore a 'perfect' sequence of words might sound unnatural


## Sampling vs Beam Search

* Outputs from beam/greedy search can sound stiff, generic, repetitive or simply boring
* That's exactly what we want from machine translation (most of the time), to exactly translate the source text without any creative variation. But it is not great for chatbots, for example
* We want them to get 'creative'