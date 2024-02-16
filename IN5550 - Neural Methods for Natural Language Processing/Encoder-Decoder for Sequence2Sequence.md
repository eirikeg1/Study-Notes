

# Problem definition
---

![[Pasted image 20240216170813.png|350]]

* We want to learn a function which maps an input sequence $X_{1:n}$ to an output sequence $y_{1:n}$
* This should work for arbitrarily long sequences for both the source and target
* **Solution**: encode $X_{1:n}$ and decode $y_{1:n}$
* Examples: translation, text to code, summarization etc.


# Encoder-Decoder models with RNNs
---
_Use one RNN to encode input to a context vector, and another RNN to decode the context vector to a new sequence_

![[Pasted image 20240216171028.png|400]]

* The generated output tokens are give by $p(t_{j+1})=f(RNN([\hat{t}_{j},c],s_{j}))$
	* Generate a token with an activation function over the RNN taking in context vector and previous state
* [[Week 1 - Linear Classifiers NLP#Softmax|Softmax]] over the vocabulary to get the actual words
* In the **Decoder**, the output token of the previous block is concatenated with the context vector $c$ from the **Encoder**. The initial block concatenates the context vector with a special $<sos>$ token


## Biggest problem

* "You can't cram the meaning of a whole fucking sentence into a single fucking vector!" - Raymond Mooney
* The **Encoder** is encoding the entire input sequence into a single vector
* This is not only conceptually problematic, but also computationally intensive
* Is often minimized by using **Attention**

## Attention for RNNs
_Search for parts of a source sentence that are relevant to predicting a target word_

* We use a weighted sum of encoder hidden states for every decoder output state
* Instead of only passing on the last hidden state as the context vector, we pass all the hidden states from the **Encoder**
* Attention weights and how they show which words are relevant to each other can be showed with an **attention matrix**:
	* ![[Pasted image 20240216174651.png|300]]

### High level explanation:
* In the decoder, for each step:
	* Calculate a score for each hidden state how relevant they are for the token it is about to generate
	* Use softmax scores to multiply with the hidden state to scale it's _importance_
	* Sum up weighted hidden states from the encoder in order to form the new context vector for the time step

### Calculations:
_There are different ways to calculate attention, this is the original one_
* Previously $c$ was constant in the prediction formula $p(t_{j+1})=f(RNN([\hat{t}_{j},c],s_{j}))$
* With attention we us a separate context $c$ for every output element $c_{j:n}$
* $c_j$ is a weighted sum of the encoder hidden states, $\alpha$ is a scaling matrix/vector
	* $c_{j}=\sum_{i+1}^{T_{x}} \alpha_{ij}h_{i}$
	* $a_{ij}$ are the softmaxed scores: $\frac{e^{e_{ij}}}{\sum_{j=1}^{K} e^{e_{ij}}}$
	* $\alpha$ is learned through training
	* **Scores** $e_{ij}$ are calculating with a scoring function (**alignment model**):
		* $e_{ij}=a(s_{i-1},h_{j})$
		* $a$ is a function that tells how relevant an input state $i$ is to an output token $j$


![[Pasted image 20240216172530.png|350]]


