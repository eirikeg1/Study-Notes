

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
* Same feature in different positions can share statistical strength (Words)
	* A token 2 words to the right and a token 2 words to the left can be one and the same word
	* Would be good for the model to use this knowledge