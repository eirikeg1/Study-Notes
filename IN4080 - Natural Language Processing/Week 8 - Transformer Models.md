
* Can be used for encoding and decoding, or both

# Types of transformers
---
## Sequence encoders with self-attention
* **BERT** model
* Contextualised word embeddings

## Sequence decoders with self-attention
* GPT
* Language modeling, text generation

## Encoder-decoder model with cross-attention
* The original transformer
* Machine translation


# Encoders
---

* For Skip-Grams With Negative Sampling, we used one target word and one context word to predict their similarity
	* Model does not see more than two words, does not know context 
		* bad for homographs/ homonyms)
		* Can't distinguish between left and right contexts, and between close and far contexts
	* Similarity prediction is practical because it enables a self-supervised setup (no data annotation needed)


# Masked language modeling
---
_Percentages can change_
* Replace 12% of tokens by blank
* In addition, replace 1.5% of tokens by another randomly chosen one
	* In order to make the _easy cases_ harder
* Train a model to 'fill in the blanks'
* 1 sentence = 1 training instance
* Self-supervised
* ![[Pasted image 20231010144202.png | 500]]

# With a simple feed forward network

* Only one word context would probably not be very good:
* ![[Pasted image 20231010144327.png | 500]]

* Adding context words, for example with sliding window is better:
* If we sum all words into the next node all words contribute equally, maybe not optimal
* ![[Pasted image 20231010144347.png | 500]]

* Ideally we want one hot encoding for all words
* ![[Pasted image 20231010144552.png | 500]]


# Self-attention
---
## Methods for computing the h layer

* **Simple average:**
	* All words count equally, not optimal
	* ![[Pasted image 20231010145010.png | 500]]
* **Weighted average:**
	* Different ways to calculate $\alpha$
		* Vector distance?
		* Content word or other word?
	* ![[Pasted image 20231010145131.png | 500]]
* **Simple type of Self-attention:**
	* Allows us to focus attention based on model training
	* $t=target\_word, c=context\_word$
	* Look at semantic similarity between $a_{(t,c)=}g_{t}\cdot g_c$
		* Dot product is a simple measure of similarity
	* ![[Pasted image 20231010145825.png | 500]]


# Self-attention
#lecture 

* We are referencing this image:
	* ![[Pasted image 20231010144552.png | 500]]

* The $g$ vectors now occur in 3 places and roles in the formula  $\alpha :softmax(g_{t}\cdot g_c)$ : 
	* As target word for computing target: $g_t$
		* We call this role query 
	* As context word for computing for context: $g_c$
		* We call this role key 
	* As a factor of the final product: (the $g_i$ in: $\alpha_{t,i} \cdot V \cdot g_i$) 
		* We call this role value
* The 3 roles are different, and the $g$ vectors are not equally well suited for all of them. 
	* Let’s create 3 different vectors tailored to the different roles

### Creating 3 different vectors

* ![[Pasted image 20231010150146.png | 500]]
* Weight values $\alpha$ can be calculated with softmax
* ![[Pasted image 20231010150325.png | 500]]

* Dot product needs to be scaled before passing to softmax, because it is better:
	* ![[Pasted image 20231010150442.png | 500]]
* Whole formula:
	* $\alpha$ matrix, key is column and value is row #Maybe 
	* ![[Pasted image 20231010150512.png | 500]]


# Multi-head attention

* Might be useful to have multiple _attention matrices_ as multiple words might be useful to find the meaning of the word
	* One for syntactic relatedness
	* One for semantic relatedness
	* One for coreference
	* etc...
* For each vector add an extra index $h$ (**head**)
	* ![[Pasted image 20231010152214.png | 500]]
* Compute the vector for one head (image has no sigmoid from top of division)
	* ![[Pasted image 20231010152300.png | 500]]
* Then concatenate all head vectors and project them:
	* ![[Pasted image 20231010152337.png | 500]]

 * One head for  each meaning:
 * ![[Pasted image 20231010152356.png | 650]]

# Position embeddings

![[Pasted image 20231010153100.png | 500]]
* Self-attention does not have any notion of word ordering
* Can be solved by adding position as position embeddings
	* Simple solution: concatenate semantic word embedding with absolute position embedding
	* Absolute numbers is not great
	* Usually we create position embeddings with several overlaid sine functions:
		* ![[Pasted image 20231010152914.png | 500]]


# Transformer blocks

#toExpand Not everything in lecture

* Multi-head self attention is not enough
* ![[Pasted image 20231010153203.png | 500]]

* ![[Pasted image 20231010153234.png | 500]]


# Usage for seq encoders

### Get contextualized word embeddings
* Train model on the MLM task
* Pass a sentence through the network and extract the _h_ vector o f each word as embedding
* Alternative: average the vectors of several layers

## Text classification

* Train model on MLM task, adding a [CLS] (class) token in front of every sentence
* Throw away the output layer, create a new one
* **Fine-Tune** the model to predict the label at the [CLS] position
* ![[Pasted image 20231010153533.png | 500]]
### Sequence labeling:
#toExpand 
* Sequence labeling (e.g. POS tagging) 
* Train a model on the MLM task 
* Throw away the output layer, create a new one 
* Fine-tune the model on POS-annotated data
![[Pasted image 20231010153741.png | 500]]


# Sequence decoders with self-attention
---

 * GPT
* Language modeling, text generation


* Difference is that no _weight arrows_ go to the right
	* Because we want to predict the _next_ word
![[Pasted image 20231010153800.png | 500]]


## Comparing with probabilistic language model

* PLM formula:
	* ![[Pasted image 20231010154108.png | 500]]
* For n-gram models, we could not condition on all preceding tokens
	* Attention can
* Typically, far-away tokens get less attention
![[Pasted image 20231010154257.png | 500]]


# Encoder-decoder models with cross-attention
---

* The original transformer
* Machine translation

* Traditional transformer:
	![[Pasted image 20231010155343.png | 700]]
# Machine translation

* Input: sentence in source language
* Output: sentence in the target language
	* Hopefully grammatical and with the same meaning
* Source and target sentence most often do not have same number of words nor the same word order

### Main idea:
* Train an encoder for source language
* Train a decoder for the target language
* In practice both are trained together with backpropagation

### Connecting encoders and decoders

* ![[Pasted image 20231010154726.png | 500]]
* Is connected with **Cross-attention:**
	* Bad when word order is difference:
		 * ![[Pasted image 20231010154844.png | 500]]
	* **Cross attention:**
		* Black vectors are self attention, red vectors are cross attention vectors
		* ![[Pasted image 20231010155000.png | 500]]

### Formula

* Dot-product attention:
	* Determines the importance of $h_j$ for $h_i$
	* ![[Pasted image 20231010155051.png | 500]]
* Context vector
	* ![[Pasted image 20231010155238.png | 350]]
