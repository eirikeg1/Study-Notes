

# Language models
---

## Why?

* Assign probabilities to sentences
	* Disambiguation?,  Reranking?
* Score the same sentence with different models
	* Language identification
	* Compute distances between languages (how similar/different)
* Predict probability of next word
	* Text completion, spelling correction
* Generate new sentences
	* Character-level n-gram language models
	* N-gram models are not useful for this, neural models are better!
* Speech recognition


## Evaluation of language models

### Extrinsic evaluation:
* To compare two LMs A and B, see how well they are doing in an application
	* Machine translations
	* Speech recognition
* Run the application with A and B, get accuracy figures, determine which one does better

### Intrinsic evaluation:
* Use a held-out corpus and measure the probabilities given to it by A and B
* The best language model is the one that best predicts the unseen corpus
* Probability $P(w_1,w_2,...,w_n)^\dfrac{1}{n}$
	* The n-root compensates for different sentence lengths
#### Perplexity:
* the inverse probability of the test set, normalised by the number of words
* For **Intrinsic evaluation:** $PP(w_1,w_2,...,w_n)=P(w_1,w_2,...,w_n)^{-\dfrac{1}{n}}$


# Probabilistic language models
---

* Assign a probability to the sentence $w_(1..n):P(w_1,w_2,w_3,...,w_n)$
	* Can only be done reliably if we have seen this exact sentence several times in the training data, which is unlikely for most sentences
* We can break the problem down by using the chain rule. This breaks the probabilities of the words into multiple smaller, easier to handle, conditional probabilities:
	![[Pasted image 20231002154737.png | 500]]


	![[Pasted image 20231002154929.png | 700]]
## Estimating probabilities

* Maximum likely estimates for a bigram LM:
	* $\hat{P}(w_i|w_{i-1})=\dfrac{Count(w_{i-1}, w_i)}{Count(w_i|w_{i-1}))}$
* We can add some smoothing: $\hat{P}(w_i|w_{i-1})=\dfrac{Count(w_{i-1},w_i)+\alpha}{Count(w_{i-1})+\alpha\cdot{|V|}}$

## Other smoothing techniques

* Additive smoothing provides non-zero probabilities for unknown n-grams
	* In many cases the words constituting these n-grams are actually known

### Backoff smoothing
* Train several models of different orders on the same data and combine them
* If you have good evidence, use the 4-gram model score, if not use the 3-gram, else the bigram, else the unigram

### Interpolation
* Always use a combination of all models with different weights:
	* ![[Pasted image 20231002161105.png | 500]]
