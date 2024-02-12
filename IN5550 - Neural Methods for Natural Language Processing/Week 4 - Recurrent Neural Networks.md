
* [[Week 3 - Count-based distributional semantic models#Use of embeddings|Embeddings]] have benefits over discrete feature vectors, can make use of unlabeled data + information sharing across features
* Embeddings does not allow you to understand sentences and documents, only words
* **RNN**s can be used to understand structured and ordered data


# What is it?

* **Recurrent Neural Networks** (**RNN**s) is a family of neural architectures
* **Input** $x_{1:n}$ is a variable lengthed sequence of elements
* **Output** $x_{1:n}$
* Internal state sequence $s_{1:n}$ as *history*
* Each state $s_i$ and output $y_i$ depend on the full previous context
	* e.g. $s_4=R(R(R(R(x_{q},s_{o}),x_2),x_3),x_4)$
* Unlike [[Week 2 - Multi-layered Networks and Deep Learning#Feed-forward neural networks|feed forward neural networks]], **RNN**s contain cycles
* **RNN**s are highly sensitive to linear order, does not need any [[Week 5 - Sequence labeling 2#Trick 2 The Markov Assumption|markov assumption]]

![[Pasted image 20240212111006.png|350]]

![[Pasted image 20240212111353.png|350]]

# Implementation
---

## The most basic implementation
_Very simple RNN, technically the same as continuous bag of words, order insensitive and no learning capabilities_

* State $s_{i}=R(s_{i-1},x_i)$
* Output value $y_{i}=O(s_{i})$
* $s_i=R(s_{i}-1,x_{})+s_{i}-1+x_i$
* $y_{i}=O(s_{i})=s_{i}$

## The Elman RNN
_Most basic type of actual RNN_

* Can actually learn dependencies between elements of the sequence, in contrast to the one above
* Instead of just summing the state and input, we multiply them with each their own weight matrix, and add bias term

![[Pasted image 20240212112242.png|500]]

![[Pasted image 20240212112308.png|250]]





## Bi-Directional Recurrent Networks

* Capture full left and right context: **history** and **future** for each $x_i$
* Moderate increase in parameters (double), still linear time computation
* ![[Pasted image 20240212113520.png|500]]

## Deep (Stacked) Recurrent Networks

* Stack multiple RNNs
* ![[Pasted image 20240212113822.png|500]]