
## Problems with static word embeddings

* The word _bank_ can have different meanings in different contexts
	* ![[Pasted image 20240212173208.png||450]]
* One solution is to represent _bank_ as the average of the word meanings
	* Problem if context words also are ambiguous
	* Also a problem when word order is not taken into consideration


# Contextualized embeddings
---
_At inference time, assign each word a vector which is a function of the whole input phrase_


* Contextualized embeddings allows the same word to have different vectors in different contexts
* Models no longer takes an isolated word, but a sequence of words
* [Website](http://vectors.nlpl.eu/explore/embeddings/en/contextual/) which lets us visualize lexical substitutes for sentences
* Embeddings are now functions based on the sequence, not a vector space with static embeddings for each word

## ELMo
_Bidirectional LSTM for making contextualized embeddings_

* Trained on raw text, optimizing for the language modeling task
* Is made up of two [[Week 4 - Recurrent Neural Networks#Bi-Directional Recurrent Networks|BiLSTM]] layers over one layer of character-based CNN #toLink 
	* Because the **LSTM** is bidirectional, each word takes all words around into account
* Takes sequences of characters (UTF-8 codes) as input
* **LSTM**s output states for each word are the ELMo embeddings
* 

![[Pasted image 20240212174230.png|400]]

### Elmo clusters the data

* 2-dimentional **PCA** projections of **ELMo** embeddings for each occurrence of the word _cell_ in the Corpus of Historical American English:
	* Left clusters: _biological_ and _prison_ senses
	* Large cluster to the right: _mobile phone_ senses

![[Pasted image 20240212174806.png|350]]

* Norwegian **ELMo** example (PCA to 2 dimensions):
	* ![[Pasted image 20240212175101.png|350]]


### Method

![[Pasted image 20240212175203.png|500]]

### Using contextualized embeddings

1. As **feature extractors**:
	* Pre trained contextualized representations are fed to the target task (e.g. document classification)
	* Conceptually the same workflow as with _static_ word embeddings
2. **Fine tuning**:
	* The whole model undergoes additional training on the target task data
	* Potentially more powerful, but computationally expensive
	![[Pasted image 20240212175651.png|400]]
