
## Classification

* L2 and L1 normalization


## Sequence labeling
* [[Week 4 - Sequence Labeling#A simple Hidden Markov model |Hidden Markov Model]]
	* States and probabilities of actions (next state)
	* HOW TO CALCULATE PROBABILITIES?
* [[Week 4 - Sequence Labeling#Viterby algorithm|Viterbi Algorithm]]
	* Used for predicting labels for a new sequence in a HMM tagger
* HMM vs Naive Bayes vs Structured Perceptron
* Transformers: Train transformer, throw away output layer, fine tune on POS-data

## Embedding relation terms

* Hypernyms and hyponyms
* The distributional hypothesis
* Tf_idf vs cosine of rows for term/doc matrix (bag of words)
* Parallelogram method for vector similarity

#### Word2vec embeddings:
* CBOW
* SKIP-grams 
	* Trained with sliding window


## Bias

* Debiasing technique, subtract differential bias word vectors (gender, race, ...)
	* Very surface level  fix

## Transformers

* Self attention formula:
	* ![[Pasted image 20231205173911.png | 250]]
	* Query, key and value vectors
		* What is the Value vector???
* 