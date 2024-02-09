
# Why?

* Creates short and dense vectors
* Easier and more efficient
* Generalize better than explicit counts
* Captures semantic relation (synonomy,...) better


# Word embeddings

* **Self-supervision**:
	* We don't manually choose distances of words which are related
	* No need for human annotation


# Neural bigram LM

* Only predicts output word based on the immediately preceding word
![[Pasted image 20231003152619.png | 500]]

## Continuous bag of words

* Concatenate and hope words are predicted properly
* Is trained by using the probability of all context words summed up as loss function
* works well but not often used
![[Pasted image 20231003152809.png | 300]]


## Skip-gram

* Learns two sets of embeddings (for target words w and context word c)
* Common to  just add them together so word i is represented by the vector $w_i + c_i$

![[Pasted image 20231003152954.png | 300]]

### Skip-gram with negative sampling
#lecture #toExpand 
* Reformulate with a binary classification
	* Output is probability 
* 

### Training gate
![[Pasted image 20231003153251.png | 500]]

* For each positive example, create $k$ negative examples:
* ![[Pasted image 20231003153328.png | 500]]

#### Computing context probabilities

* You can compute similarity using dot product
* Using activation function to convert this to probability (e.g with sigmoid)
* In order to get these vectors we can initialise the vectors with random values

#### Training:
* Randomly initialize two vectors for each word of the dataset 
	* One for its use as target word (w) 
	* One for its use as context word (c) 
* Pick an example from the training data (positive or negative) 
* Predict probability 
* Compute loss and update vectors based on gradient 
* Pick next example
* ![[Pasted image 20231003153825.png | 500]]


### Effect of window size

* Small windows (+-2 context words) gives syntactically similar words of same taxonomy (part of speech)
* Large windoes (+- 5 cws) gives related words in same semantic fields

#### Analogical relations

![[Pasted image 20231003154444.png | 500]]

![[Pasted image 20231003154556.png | 500]]

Can be applied to morphalogical relationships as well
![[Pasted image 20231003154842.png | 500]]

Can also be used to see how word meanings have changed through the years
![[Pasted image 20231003154947.png | 500]]


#### Analytical relation biases

* Problems can occur if data is biased or unbalanced
* Male and female terms can end up relatively far apart
* ![[Pasted image 20231003155045.png | 500]]

#### Debiasing

* Identify pairs of words that does not have any particular bias
* Can be done by e.g removing the _differential word_ to each respective value
* Can reduce bias but might be a very surface level fix
* ![[Pasted image 20231003155222.png | 500]]


## Insintric evaluation
_Datasets to evaluate embeddings_