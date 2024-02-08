

# Discrete features
---
_Using discrete features means each feature is completely independent from each other_

* **One-hot encoding** is one way, by adding all terms to an indexed vector. A vector of similar size is the feature input, where the value of each index represents how many times the relative term appears in the document. Is a [[Week 2 - Classification 2#Bag of words|bag of words]] implementation


## Pros

* Efficient to compute
* Often good enough for simple tasks

## Cons

* Features are extremely sparse, as the feature size is the entire vocabulary/categories
* Classifiers have to learn weight matrices with dim = $|V|$ (entire vocabular)
	* Is not efficient as other methods only require the actual features present in the document


## Reducing dimensionality

* **The curse of dimensionality**: When we have a lot of dimensions (one per term in vocabulary) the vectors can be very sparse
* It is possible to reduce vector sizes to some reasonable values, and still preserve meaningful relations between them
	* For example by **factorizing the co-occurrence matrix**, using **PCA** or other dimensionality reduction techniques
* By reducing the dimensionality the vector components are no longer directly interpretable, meaning you don't exactly know what each dimension represents, but it can still give useful clustering
	![[Pasted image 20240208190514.png|300]]]

# Continuous features
---
_Embed terms in a vector space, gives features representations relative to each other_

* Can give much denser vectors
* Components can be viewed as  coordinates in an n-dimensional space
* Dimensionality $d$ can be much lower than $|V|$, for example $|V|=100.000, d=100$
* Values are learned during training

## Pros

* Dimensionality representations are usually low (50-300)
* Feature vectors are dense, not sparse (computationally efficient)
* Generalization power: similar entities get similar embeddings (hopefully)
	* *Town* should be closer to *city* then *banana*
* Same feature in different positions can share statistical strength (words right beside each other are often very similar)
	* A token 2 words to the right and a token 2 words to the left can be one and the same word
	* Would be good for the model to use this knowledge


## Dependency parsing
_Building a syntactic tree based on word relationships_


* *flight* and *me* are children of *Book*
* Parses in several steps
* Conceptually it is the classic **Arc-Standard transition-based parser** 
* Uses dense embeddings for words, PoS tags and dependency labels
![[Pasted image 20240206114432.png|400]]


# Use of embeddings
---

* [[Week 6 - Word vectors and embeddings|Word vectors and embeddings]]
* Concatenated embeddings of **words** $x^w$, [[Week 4 - Sequence Labeling#Part-of-speech tagging (POS)|POS tags]] $x^t$ and **dependency labels** $X^{l}$ from the stack are given as input layer
* Embeddings are trained with gradient descent
	* to minimize he cross-entropy loss $L(\theta)$
	* to maximize the probability of correct transitions $t_i$ in a collection of $n$ configurations
	* Model employs the unusual **cube activation function** $g(x)=x^3$
