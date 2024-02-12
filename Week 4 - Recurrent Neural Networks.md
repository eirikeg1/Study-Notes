
* [[Week 3 - Count-based distributional semantic models#Use of embeddings|Embeddings]] have benefits over discrete feature vectors, can make use of unlabeled data + information sharing across features
* Embeddings does not allow you to understand sentences and documents, only words
* **RNN**s can be used to understand structured and ordered data


# What is it?

* **Input** $x_{1:n}$ is a variable lengthed sequence of elements
* **Output** $x_{1:n}$
* Internal state sequence $s_{1:n}$ as *history*
* Each state $s_i$ and output $y_i$ depend on the full previous context
	* e.g. $s_4=R(R(R(R(x_{q},))))$
* Unlike [[Week 2 - Multi-layered Networks and Deep Learning#Feed-forward neural networks|feed forward neural networks]], **RNN**s contain cycles
* **RNN**s are highly sensitive to linear order, does not need any [[Week 5 - Sequence labeling 2#Trick 2 The Markov Assumption|markov assumption]]

![[Pasted image 20240212111006.png|300]]

![[Pasted image 20240212110537.png|300]]


## 

