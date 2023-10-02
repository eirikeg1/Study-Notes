_Used to capture and represent the meaning of words_


# The meaning of words:

* A word (**lemma**) can have multiple meanings/definitions (**sense**). 
* Words with several senes are called  **polysemous**
* If two words sound/look the same they are **homonyms**
* Could make vectors with a dimension for each sense #Maybe 

## Relations between senses

* Different senses of a word can be related in various ways
* **Synonyms** and **antonyms**
* **Hyponyms** and **hypernym** 
	* Word pairs fex.: rose -> flower, car -> vehicle
	* Transitive relations
	* ![[Pasted image 20231002170144.png | 350]]
* Less well defined relations:
	* **Similarity**: 
		* Word with the same hypernym (cow-horse, boy-girl)
		* second order association: the relationship is not directly between two words, but they have a common relation
	* **Relatedness**: 
		* (money-bank, fish-water)
		* first order association: has a direct assocition
* ![[Pasted image 20231002171036.png | 700]]

# Vector semantics
---

## Distributional word representations

### The distributional hypothesis:
_The meaning of a word can be captured by the contexts in which it occurs_

## Calculating similarity (cosine similarity)
* Represents the angle between two vectors
* Length of vector does not matter
* 
	![[Pasted image 20231002174943.png | 700]]

## Core  idea

* Each word is represented as a point in a multidimensional semantic space (word vectors/embeddings)
* The points are inferred from the distributions of word neighbors/contexts in text, according to the distributional hypothesis
* Similar/related words are close to each other in this space
* 2d example:![[Pasted image 20231002171837.png|700]]

# How to create vectors

## Word-document (term-document) matrices
_matrices based on co-occurrence counts, count weighting of tf-idf_
 
* One row per term/word, values represents counts of terms in document
* This table is similar to the bag of words approach, used in Naive Bayes
	* ![[Pasted image 20231002172428.png | 500]]
#### Uses:
* Compute similarity between words:
	* Fool and wit are similar
	* ![[Pasted image 20231002180406.png | 500]]
* Compute similarity between documents:
	* _As you like_ and _Twelfth night_ are similar (comedies)
	* _Julius Caesar_ and _Henry V_ are similar (historical dramas)
	* ![[Pasted image 20231002180434.png | 500]]
* Information retrieval:
	* Encode query as an additional document
	* Find documents that are most similar to query

#### Count weighting with tf-idf
_Not all words are equally important_

![[Pasted image 20231002182547.png | 500]]

* **Term Frequency** multiplied by **Inversed Document Frequency**
	* $tf_{t,d}\cdot \log{\dfrac{N}{df_t}}$
* **Term Frequency**
	* $tf_{t,d}$ is the frequency of term $t$ in document $d$
* Document Frequency
	* $df_{t}$ is the number of documents containing term $t$
	* **The Inverse Document Frequency** is one divided by the document frequency
	* Normalize by collection size $\dfrac{N}{df_t}$
	* By convention, take the log: $\log{\dfrac{N}{df_t}}$
* Intuition: a word occurring in a large proportion of documents is not a good discriminator for the meaning/context behind the words
	* In the example of the _tf table_ above the word _good_ does not contribute much to distinguishing between documents
	* Importance of a word should be inversely proportional to the number of documents in it
* In python, replace **CountVectorizer** with **TfIdfVectorizer**


## Word-context matrices
_Based on co-occurrence counts, is more used than TermFrequency method _

* Dimensionality reduction (SVD, LSA)
* One row per term/word
* One column per context term/word (rows and columns can be the same but not necessarily)
* Vales represent counts of words *within the context* of another word

#### What is the context?
_Multiple definitions_

* Words in the same sentence
* $n$ words to the left and right
	* Often stopwords are not counted ($n$ words to the side excluding words like of/the)


#### Uses:

* Compute cosine similarity between words
* Compute cosine similarity between context words (usually columns but can also be done on rows)

### Dimensionality reduction

* Most word-context vectors are sparse and take up a lot of space/computation and lacks generalisation capabilities
	* Most values are 0, especially in  small context sizes
* Reduce the number of columns to a fixed size $m$ (typically in the range 50-500)
	* Uses **Singular Value Decomposition** (**SVD**)
	* ![[Pasted image 20231002184433.png | 500]]
* The new columns represent abstract properties, not words
* The combination of **SVD** dimensionality reduction with word-context vectors is known as **LSA** (**Lagent Semantic Analysis**)
* Other combinations are possible e.g. using **PCA** (**Principle Component Analysis**)
* Typically 100-500 target dimensions, but can use as few as 2 for visualization

## Alternative approaches for word embeddings

* For example Neural network based (**word2vec**)
	* A direct way to get dense word-context vectors
* More recent developments:
	* **FastText**
	* Contextualised embeddings: **BERT**
		* Difference between **BERT** and **word2vec** is that **BERT** gives different vectors to the same word based on it's context, **word2vec** always gives the same vector to a given word
* Python module *gensim* is useful for all kinds of word-vector-related experiments


### Word embeddings



