
# Part-of-speech tagging (POS)
---
*Give a word a basic grammatical category*

* Has traditionally been useful for preprocessing
* Good for capturing semantics
* Can be visualized in **Verticalized format**:
	![[Pasted image 20230912143717.png | 500]]


## Tag sets

* Different languages might have multiple tag sets, but there is an universal one with 17 categories
* **Universal POS tag set**: ADJ, ADV, INTJ, NOUN, PROPN, VERB, ADP, AUX, CCONJ, DET, NUM, PART, PRON, SCONJ, PUNCT, SYM, X

![[Pasted image 20230912144305.png | 750]]

## Ambiguity of tags
#toExpand 
![[Pasted image 20230912144932.png | 750]]


# Sequence labeling
---
## Goal
* Predict a label for each element of a sequence 
* I.e. predict a label for each word of a sentence 
* Easy cases: 
	*  Unambiguous words (words seen together with a single label during training)
*  Difficult cases:
	* Unknown words (words not seen during training) 
	* Ambiguous words (words seen together with several labels during training)


# Named entity recognition

* An entity is when you can have multiple words in one token based on content
![[Pasted image 20230912145442.png | 750]]

### Example
* Can be problematic if *washington* is the city or name
![[Pasted image 20230912145545.png | 500]]
![[Pasted image 20230912145559.png | 500]]

## BIO encoding

* B = Beginning of new entity
* I = Inside an existing named entity 
* O = Outside of any named entity

![[Pasted image 20230912145804.png | 700]]


# Generative Sequence Models
---

# Different ways to look at the context

## Option 1: look at neighboring words:
* ![[Pasted image 20230912153339.png | 500]]
* Does not work with generative learning algorithms
* Works well with discriminative algorithms


## Option 2: look at the previous tag decisions
* Works well with #toExpand 


# Naive Bayes for sequence labeling

* Unigram model (can only give the same answer to a word all the time regardless of context)
* 

## A first and (probably bad) way:
* Look at one word at a time without context and pick a tag
* Prediction function: ![[Pasted image 20230912151733.png | 500]]
* Probabilities from training data: ![[Pasted image 20230912151808.png | 500]]
* Will not take context in mind, for example in the sentence *cats fish fish* where second word should be a verb this will give the same category to both. Any ambiguous words will not be caught



### Smoothing
_Can be used to deal with unknown words_

**Option 1: add-one smoothing:** ![[Pasted image 20230912152318.png | 500]]

**Option 2: use rare words classes:**
* Split vocabulary into two classes rare or frequent words.
* Replace all rare words in training data by _rare_ before computing probabilities
* Replace unknown words in test data by _rare_


# Generative unigram/bigram models

**Unigram models calculate every word independently:**
![[Pasted image 20230912152824.png | 500]]

**Bigram models usually use the priors:**
![[Pasted image 20230912152851.png | 500]]

**It is possible to make Trigram models as well:**
*Example of Trigram Hidden Markov Model*
![[Pasted image 20230912153130.png | 500]]

# A simple Hidden Markov model

#toExpand 
* Similar to Naive Bayes prediction function: ![[Pasted image 20230912152944.png | 500]]
* Replace the prior probabilitiy by conditional probability: ![[Pasted image 20230912153024.png | 500]]
* Is a transition probability which is the probability of going from previous class to current (fex noun to verb)
* #toExpand 

## Computing probabilities
* One argmax per position ![[Pasted image 20230912154138.png | 500]]


## Problems
* *Fish dogs like cats*
* Strongly bias to N - V - N - V sequences
* Some patterns ruin sequences, which affects future predictions
* When a model goes wrong it has problems getting back on track


## Fixing the problem
* **Exact inference/decoding**:
	* Compute all possibilities and choose the most probable one
	* Very resource intensive on big datasets, grows by the power of words
	* Can be improved with **The Viterbi algorithm**


## Viterby algorithm
* A lot of the computations will be duplicates ![[Pasted image 20230912155617.png | 750]]
### Trick 1: Decomposing the product
* Proceed one position at a time and save intermediate results ![[Pasted image 20230912155828.png | 750]]
### Trick 2: The Markov assumption

* There are ways to remove steps which probably give a bad result
* ![[Pasted image 20230912160116.png | 750]]




