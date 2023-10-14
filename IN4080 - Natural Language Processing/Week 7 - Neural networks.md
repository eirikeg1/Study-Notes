
![[Pasted image 20231003143534.png | 650]]
# Linear models for producing embeddings
---

## Text classification:

![[Pasted image 20231003142507.png | 500]]

### Training

![[Pasted image 20231003142551.png | 500]]


# Multi-class linear models

* each output corresponds to a class
* Uses probability distribution **activation function** like for example softmax

![[Pasted image 20231003142725.png | 500]]


## Two-step classification

* Partition collection into e.g. 100 text classes
* Base sentiment decision on the text class
* Kind of like to classifiers where the output of one is the others input

* ![[Pasted image 20231003143012.png | 300]]

## Activation functions

### Softmax
* Gives probaility distribution
* Costly

### Sigmoid
* Binary
* ![[Pasted image 20231003143320.png | 400]]
### Tanh
* Similar to sigmoid but often better
* ![[Pasted image 20231003143411.png | 300]]

### Relu
* Very simple and often used
* ![[Pasted image 20231003143450.png | 300]]

# Training
#lecture 
* • For every training tuple (x,y): 
	* Run forward computation to find our estimate y-hat
	* Run backward computation to update weights: 
		* For every output node: 
			* Compute loss � between true � and the estimated �, 
		* For every weight � from hidden layer to the output layer: 
		* Update the weight 
	* For every hidden node: 
		* Assess “how much blame it deserves for the current answer” 
		* For every weight � from input layer to the hidden layer: 
			* Update the weight

![[Pasted image 20231003145734.png | 500]]


## Gradient descent for LR

![[Pasted image 20231003150014.png | 500]]

# Loss

* For binary logistic regression, we typically use the cross-entropy loss:
* ![[Pasted image 20231003145916.png | 500]]
* 

# Feed forward neural networds
---
![[Pasted image 20231003145343.png | 350]]
![[Pasted image 20231003145402.png | 350]]
* Arrows go up
* Also called **multi-layer perception**
* input units $x_i$, hidden units $h_i$

## Binary or Multinomial

* binary only have one output layer after last hidden node layer, the rest does not have to have it
* ![[Pasted image 20231003145537.png | 500]]

## Hidden layers

* Used to get a non-linear decision boundary #Maybe 
* Example is the **XOR problem**


### AND/OR problems

* Linear boundaries works well for AND and OR, but not XOR
* ![[Pasted image 20231003144300.png | 500]]


### XOR-problem 
#lecture
* People have either light or dark hair 
* People have either light or dark eyes 
* People are right-handed whenever their hair and eye color matches, and left-handed when it doesn’t match
* ![[Pasted image 20231003144000.png | 500]]


## Extended features

* Sometimes adding extra features can make a non-linearly separable data set linearly separable, but not always
* Usually you have to find it out using logic manually
* Neural networks can similar to this automatically
* ![[Pasted image 20231003144420.png | 500]]

## XOR in neural networks

 * Each column is different inputs for $x$
![[Pasted image 20231003144806.png | 700-]]


### How?

* Only works for particular set of weight $W$ and $U$
* Moves the points in the space
![[Pasted image 20231003145029.png | 700-]]

# Training
_Similar to linear gradient descent_

* Uses the **chain rule** for **backpropagation**
* Calculate the derivative of the loss with respect to each weight in every layer of the network
* _Distributes_ the loss gradient over all layers
* Uses a computation graph
* ![[Pasted image 20231003150117.png | 500]]


#### Computation graph: 
![[Pasted image 20231003151750.png | 500]]
![[Pasted image 20231003151815.png  | 500]]

#### Backpropagation in a two-layer network
![[Pasted image 20231003151944.png | 500]]



# Neural document classification

* Document classification - one vector per doc
* Word embeddings - one vector per word

## Pooling

* Combine all word vectors into a doc vector
* Concatenate all word vectors
* Take mean of all word vectors



# Neural language models using vectors
---


## Prediction using sliding window

* Serious drawbacks:
	* Not efficient, each word run several times
	* Context limited to window size
* Still neural LMs work better than probabilistic
	* Neural networks can predict based on semantic similarity, even if not in training set:
	* ![[Pasted image 20231010143139.png | 500]]
* ![[Pasted image 20231010142750.png | 500]]


