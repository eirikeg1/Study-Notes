

![[Pasted image 20230919153743.png | 700]]
# Greedy vs Viterbi
* Greedy is usually good enough, for much cheaper

# Bigram Hidden Markov Models
---

## Training 
* For each $x,y$ in training data: 
	 * Compute and store: ![[Pasted image 20230919141956.png | 350]]
* For each bigram $y_{i-1}, y_i$ in training data: 
	* Compute and store: ![[Pasted image 20230919142127.png | 350]]

## Prediction
For each sentence in test data: ![[Pasted image 20230919142211.png | 500]]


## Trick 1: Dynamic programming

* There are multiple duplicate computations, calculate once and reuse
* ![[Pasted image 20230919142329.png | 500]]
* Store intermediate results as $pi$:
* ![[Pasted image 20230919142425.png | 350]]
* ![[Pasted image 20230919142513.png | 500]]

## Trick 2 The Markov Assumption

* Identify unpromising sequences and ignore them
* ![[Pasted image 20230919142627.png | 500]]

**Bigram Markov assumption looks at the probabilities of the last word:**
* ![[Pasted image 20230919143116.png | 500]]

### Example with trigram (comparing three at a time):
![[Pasted image 20230919143627.png | 700]]
N and V below says what is predicted on the meeting column
![[Pasted image 20230919144345.png | 700]]
**Use backpointers to find highest probabilities, with the Viterby algorithm:**
![[Pasted image 20230919144602.png | 700]]


# Viterbi algorithm
*Recursive optimal solution to the problem of estimating the state sequence of a discrete-time finite-state Markov process*

* Use table $\Pi[k,y_k]$ to store computations
	* Contains max probabilitiy for sequence $x_1 .. x_k$ ending in tag $y_k$
* Initialization:
	* $\Pi[0,*] = 1$
* Recursive definition:
	* Fill $\Pi$ for all positions $k\in{\set{1 ... n}}$ and all labels:
	* $\Pi[k,y_k]=max/{y_{k-1}\in Y}$ 

![[Pasted image 20230919144759.png| 700]]

* $*$ to mark the start of the sentence, _cross sign_ to mark end
![[Pasted image 20230919144914.png | 500]]

# Previous probabilities or neighboring words
---
* Neighboring words usually creates rules that two types always come together
* Previous words usually lowers probabilities of two words which rarely comes

**Combining the two**
![[Pasted image 20230919145504.png | 500]]

## Context word features for finding probabilities of neighbouring words

* $f_x$ represents a one-hot vector:
	![[Pasted image 20230919145928.png | 350]]
* Orange is previous word, black is current, green is next:
![[Pasted image 20230919145722.png | 700]]

### You can add manual sentence-level features:
*  Features for unknown words:
	* $x_i$ contains a particular prefix 
	* $x_i$ contains a particular suffix 
	* $x_i$ contains a number 
	* $x_i$ contains an upper-case letter 
	* $x_i$ contains a hyphen 
	* $x_i$ is all upper case 
	* $x_i$ is upper case and has a digit and a dash
	![[Pasted image 20230919150048.png | 500]]


# Structured Perceptron
---
_Combines neighbouring and previous tag_

![[Pasted image 20230919153041.png | 700]]
## Transition features
	![[Pasted image 20230919152704.png | 500]]
* We don’t actually need to build an explicit transition feature vector • The transition weights can be thought of as a Y×Y matrix (as in HMMs):
	* ![[Pasted image 20230919153017.png | 250]]
* The transition feature just selects one column of this matrix
* 

## Greedy variant
_Orange=transition, blue=emission_
	![[Pasted image 20230919153143.png | 500]]
* Contains **transition**- and **emission-features**
* Emission features can be arbitrarily complex 
* Transition features: one-hot vector with $|Y|$ items:
	![[Pasted image 20230919152817.png | 350]]

## Exact (Viterbi) variant
	![[Pasted image 20230919153229.png | 500]]
* Similar to Viterbi for HMMs
* Main operations are sums, so base case is 0, not 1
	
## Training
* Take one training instance and predict
	* if the prediction is correct nothing happens
	* if wrong add feature values to weights of correct vector and subtract from wrong
* Continue until tired
	![[Pasted image 20230919153638.png | 750]]

# Sequence labeling logistic regression models (CRF)
_Conditional Random Fields_

![[Pasted image 20230919153923.png | 700]]

* Same features as Structured perceptron
* Uses Stochastic gradient descent
* Uses Viterbi algorithm

## Prediction

**If we are only interested in the argmax:** 
* we can get rid of the denominator 
* we can get rid of the exponentiation 
* the prediction function becomes identical to the structured perceptron one. 
* ![[Pasted image 20230919154259.png | 500]]

### Formula explanation
* $\max \sum_{i=1}^{N} \left( w_t(y_i, y_{i-1}) + w_E(y_i) \cdot f_E(x_i) \right)$

- $\max$ denotes the maximization over all possible label sequences.
- The summation$\sum_{i=1}^{N}$ iterates over each element $i$ in the sequence, from 1 to $N$, where $N$ is the length of the sequence.
- $w_t(y_i, y_{i-1})$ represents the transition weights from the previous label $y_{i-1}$ to the current label $y_i$.
- $w_E(y_i)$ are the weights for the emission features corresponding to label $y_i$.
- $f_E(x_i)$ is the emission feature vector for the $i$-th element of the input sequence $x_i$.
- The term $w_E(y_i) \cdot f_E(x_i)$ calculates the dot product between the emission feature vector and the corresponding weights for label $y_i$, providing a score based on how well the input features at position $i$ match the label $y_i$.

This formula is used in structured prediction models for sequence labeling, combining both the emission and transition aspects to capture the sequential dependencies in tasks such as part-of-speech tagging or named entity recognition.

**But sometimes we are interested in the probabilities:** 
* for training (update) 
* for model analysis 
* for semi-supervised learning. 

## Parameter estimation
* We can take $Z$ out of the max
	![[Pasted image 20230919154518.png | 700]]
* Computationally expensive



# Maximum Entropy Markov models
---
*Simpler alternative to CRF*

* Instead of having sum inside exponent, have it outside
* More efficient to train, but worse performance	![[Pasted image 20230919154848.png | 700]]

