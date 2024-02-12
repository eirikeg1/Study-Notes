
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

# Simple RNNs
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

* In practice multiple RNNs stacked after each other
* Each layer's state is isolated from each other apart from output/input, but trained together at the backpropagation step
* ![[Pasted image 20240212113822.png|500]]


# Gated Recurrent Neural Networks
---
_Architecture used to prevent exploding/vanishing gradient problem_

* Used to prevent [[Week 2 - Practicalities and hyper-parameters#Exploding- / Vanishing gradient problem|exploding/vanishing gradient problems]]

![[Pasted image 20240212153307.png|450]]

## Gate filtering

* **Hadamard product** $\odot$  simply performs element-wise multiplication
* vector $g$ acts as a **gate**: masks out parts of the memory and input
* **Gates** are differentiable so they can be trained, but when using them are squashed to either 1 or 0 using for example a [[Week 7 - Neural networks#Sigmoid|sigmoid function]].
* **Gates** are used to determine if you should use the value $s_i$ or $g_i$ for each $i$ in $s'$
* In diagram below, we take the values from $x$ where $g$ is 1, replace the rest with values from the state $s$
* ![[Pasted image 20240212150920.png|350]]

## Long Short-Term Memory RNNs (LSTMs)

* State vectors $s_i$ partitioned into **context memory** and **hidden state**
* Forget gate $f$: how much of the previous memory to keep
* input gate $i$: how much of the proposed update to apply
* output gate $o$: what parts of the updated memory to output
* Therefore we have more parameters than in a simple **RNN**, with separate $W^{x\cdot}$ and $W^{h \cdot}$, matrices for each gate as well as bias vectors

![[Pasted image 20240212151812.png|450]]

![[Pasted image 20240212152956.png|350]]


## Gated Recurrent Units (GRUs)
_More modern simpler variant of LSTMs_

* No separate context memory
* Less gates
![[Pasted image 20240212153105.png|350]]



# Tips and tricks
---

* Although **RNN**s in principle are well-defined for inputs of variable length, in practice **padding** to a fixed length is required for efficiency (batching). Actually not too much *waste*, but can be beneficial to bin by length to minimize padding
* **Accuracy** is a common metric for tagging; fixed number of predictions. For most inputs, very large proportion of padding tokens (and labels)
* Trivial predictions will inflate the accuracy scores, which can be detrimental to learning
* Can define custom accuracy functions, mask padding tokens predictions

## What to use for classification?
* The last hidden state?
* The sum or the average of each element states?
* **Max Pooling?**
	* Take the highest value for each vector index from all the words
	* Allows you to use the _most excited neurons_
	* ![[Pasted image 20240212172637.png|300]]

## Dropout in RNNs

* Dropout along memory updates can inhibit learning of effective gating
* Randomly sets weights to zero in order to make sure the model does not rely to heavily on certain neurons
* Similar concept to [[Week 2 - Practicalities and hyper-parameters#Dropout|dropout in feed forward neural networks]]
* only apply dropout _vertically_ or fix random mask (**veriational RNN**)
* ![[Pasted image 20240212172816.png|400]]