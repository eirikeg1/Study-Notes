
## The distributional hypothesis
_Word that occur in similar contexts tend to have similar meaning_

* The basis for distributional models
* Key concept is to train embeddings so that every term embedding becomes more 'similar' to its neighboring context words in the corpus



# Predictive approaches using neural language models
---

* We try to find (predict) for each word a vector/embedding such that it is
	* Maximally similar to the vectors of its paradigmatic neighbors
	* minimally similar to the vectors of the words which in the training corpus are not paradigmatic (words uses in the same context like dog and cat) neighbors of the given word
* [[Week 6 - word2vec embeddings|word2vec embeddings]]
* [Demo of word2vec algorithms](https://ronxin.github.io/wevi/)
* ![[Pasted image 20240208192038.png|400]]
* ![[Pasted image 20240209171048.png|400]]

## Training

* During **word2vec** training we have to take all words in $V$, calculate their dot products with the current prediction, and then produce a probability distribution with [[Week 7 - Neural networks#Softmax|softmax]]
* The vector of a word $w$ is _dragged_ back and forth by the vectors of $w$'s co-occuring words, as if there are physical strings between $w$ and it's neighbors

## Hierarchical softmax

* Rarely used


## Negative sampling (Noise-Contrastive Estimation)
_Choose a few random words during training, which are not context words, update their weights accordingly_
[[Week 6 - word2vec embeddings#Skip-gram with negative sampling|]]
* [[Week 6 - word2vec embeddings#Skip-gram with negative sampling|Skip gram with negative sampling]]
* Sample a few (e.g. 5..15) random 'noise' words from $V$, which serve as **negative examples**
* Dealing with 15 word pairs is much faster than applying softmax to the full vocabulary


## Pretrained word embedding  models

* Can come in several formats
	1. **.txt**, **.vec**
		* words and sequences of values representing their vectors, one word per line
		* the first line gives info on number of words in the model and the vector size
	2. Binary form **.bin**
		* more compact, but can't read the content manually
	3. **Gensim format**
		* Uses **NumPy** arrays
		* Recommended
		* Stores additional info (training weights, hyper-parameters, word frequency, etc.)
		* On [[Fox data cluster cheat sheet|Fox]]: 
		```Shell
		module load nlpl-gensim/4.3.2-foss-2022b-Python-3.10.8
		```


# Types of models
---
## Continuous Bag Of Words (CBOW)
_Model which outputs a vector embedding of a word based on its context_

* [[Week 6 - word2vec embeddings#Continuous bag of words|CBOW IN4080]]
* At each training instance, the input for the prediction is the average input vector for all context words. We check whether the current word output vector is the closest to it among all vocabulary words
* Returns an vector embedding representing the semantic meaning of the word, based on its context words
* **Loss function**: 
	* $c$ are the context words
	* $L=-\log{(P(w_{t}|\sum\limits_{i=t}^j c_{i}))}$




## Continuous Skip-Gram (skipgram)
_Predicts a term based on its context (vector embedding)_

* At each training instance, the input for the prediction is the current word input vector. We check whether each of the context words is the closest to it among all vocabulary words
* Returns the term (usually **one-hot encoded**) based on the input vector
* Closeness is calculated with the help of dot product or cosine similarity and turned to probability using [[Week 7 - Neural networks#Softmax|softmax]]
* [[Week 6 - word2vec embeddings#Skip-gram with negative sampling|Skip grams with negative sampling]] (**SGNS**) is still often used, despite the newer pretrained [[Week 8 - Transformer Models#Sequence encoders with self-attention|Transformer-based language models]] like **Bert**
* **Loss-function**:
	* ![[Pasted image 20240209172404.png|300]]


## fastText


# Hybrid approaches
---