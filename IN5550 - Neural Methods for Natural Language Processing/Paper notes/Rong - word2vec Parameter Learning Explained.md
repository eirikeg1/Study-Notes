

# Summary

* [PDF](https://arxiv.org/pdf/1411.2738.pdf)
* Gives an detailed explanation of how [[Week 3 - Machine learning based distributional models#Continuous Bag Of Words (CBOW)|CBOW]] and [[Week 6 - word2vec embeddings#Skip-gram|skipgrams]] are implemented
* Gives advanced optimization techniques like **hierarchical softmax and negative sampling**
* Gives all the formulas and calculations along the way
* [Wevi](https://ronxin.github.io/wevi/) - interactive model to understand the model

## Abstract
_The word2vec model and application by Mikolov et al. have attracted a great amount of attention in recent two years. The vector representations of words learned by word2vec models have been shown to carry semantic meanings and are useful in various NLP tasks. As an increasing number of researchers would like to experiment with word2vec or similar techniques, I notice that there lacks a material that compre hensively explains the parameter learning process of word embedding models in details, thus preventing researchers that are non-experts in neural networks from understanding the working mechanism of such models. This note provides detailed derivations and explanations of the parameter up date equations of the word2vec models, including the original continuous bag-of-word (CBOW) and skip-gram (SG) models, as well as advanced optimization techniques, including hierarchical softmax and negative sampling. Intuitive interpretations of the gradient equations are also provided alongside mathematical derivations. In the appendix, a review on the basics of neuron networks and backpropagation is provided. I also created an interactive demo, wevi, to facilitate the intuitive under standing of the model._


# Continuous Bag-of-Word model

* [[Week 3 - Machine learning based distributional models#Continuous Bag Of Words (CBOW)|From IN5550]]
* Input: one-hot encoded vector


# Skipgrams



# Optimizations
---

* Learning input vectors is chearp, output vectors is very expensive
* In order to updata $v'$ we have to iterate through every word $w_j$ in the vocabulary, compute theri net input $u_j$, probability prediction $y_j$, theier prediction error $e_j$ and finally use their prediction error to update their output vector $v'_j$
* To solve this problem we can limit the number of output vectors that must be updated per training instance

## Hierarchical Softmax
_Efficient way of computing softmax. Uses binary tree to represent all words in vocabulary_

* The $V$ words in the vocabulary must be leaf nodes in the tree
* For each leaf unit there exists a unique path from the root to the unit, this path is used to estimate the probability of the word, represented by the **leaf unit**
* In the image below the white nodes are words in $V$ (**leaf units**, while the dark nodes are **inner units**:

![[Pasted image 20240209190354.png|400]]
* There are $V-1$ inner units

* There are no output vector representation for words, instead each of the $V-1$ inner units has an output vector $v'_{n(w,j)}$
* Probability of a word being the output word is:
	* ![[Pasted image 20240209190800.png|400]]
	* 

## Negative sampling