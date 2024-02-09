


# Predictive approaches using neural language models
---

* We try to find (predict) for each word a vector/embedding such that it is
	* Maximally similar to the vectors of its paradigmatic neighbors
	* minimally similar to the vectors of the words which in the training corpus are not paradigmatic (words uses in the same context like dog and cat) neighbors of the given word
* [[Week 6 - word2vec embeddings|word2vec embeddings]]
* ![[Pasted image 20240208192038.png|400]]
* ![[Pasted image 20240209171048.png|400]]
## Continuous Bag Of Words (CBOW)
_Model which outputs a vector embedding of a word based on its context_

* [[Week 6 - word2vec embeddings#Continuous bag of words|CBOW IN4080]]
* At each training instance, the input for the prediction is the average input vector for all context words. We check whether the current word output vector is the closest to it among all vocabulary words



## Continuous Skip-Gram (skipgram)
_Predicts a term based on its context (vector embedding)_

* At each training instance, the input for the prediction is the current word input vector. We check whether each of the context words is the closest to it among all vocabulary words
* 


## fastText




# Hybrid approaches
---