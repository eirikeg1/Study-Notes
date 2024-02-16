
# Summary
---
## Some practical things to take into consideration:

1. Depth (number of hidden layer)
2. Width (Number of nodes in each layer)
3. Non-linearity
4. Initialization strategy
5. Normalization
6. Optimization algorithm
7. Learning rate
8. Batch size
9. etc...

## How to explore different hyperparameters
_Different methods for finding the optimal hyperparameters_

* **Grid search**
	* Try all combinations
* **Random search**
	* Try random combination
* **Bayesian search**
* **[[Week 2 - Classification 2#K-fold cross-validation|K-fold cross validation]]**
* Trial and error


# Depth
---
_Refers to how many layers are in the model_

* In computer vision, models are often hundreds of layers deep
* In NLP often varies between 1-2 up to 24 (**BERT**) or even 78 (**Turing-NLG**)
* The strongest NLP models are still growing in depth, but it's not entirely clear how much extreme depth benefits

## Deeper can give more accurate results

* Deeper models leads to more capacity (parameters) and more complex functions
* Deeper can also lead to overfitting
* Making a network deep can lead to the **exploding** and **vanishing gradient** problems

![[Pasted image 20240129152804.png|650]]


# Exploding- / Vanishing gradient problem
## Vanishing gradients
_Very deep neural networks can have problems with learning_

* As gradients flow through deep neural networks, it can tend towards zero (**vanishing gradient**)
* This is because back-propagation computes the gradients by the chain rule
	* When multiplying multiple small numbers, the number becomes exponentially small
	* Therefore the model learns very slowly, or stop learning completely
* For example does the [[Week 7 - Neural networks#Sigmoid|sigmoid function]] have very low derivatives at the end 
* ![[Pasted image 20240129153109.png|600]]

## Exploding gradients

* If you have a non-linearity whose derivatives can take larger values, the gradients become overly large (explode)
* Training will then make too large changes to the parameters
* Makes learning very unstable, or not working at all


# Improving model training/result
---

## Choosing the non-linearity of hidden layers
_Different activation functions have different properties_

* Usually this is the best order for hidden layer [[Week 7 - Neural networks#Activation functions|activation functions]]
	1. ReLU
	2. Tanh
	3. Sigmoid
* Many other new options (maxout, gelu, elu)


## Initialization parameters

* Usually it is normal to start with very small random numbers
* If initialized to 0 the model can have problems with starting to learn
* The randomized initial values can help with the exploration
* In PyTorch the initialization depends on the kind of layer that you are instantiating, [initialization docs](https://pytorch.org/docs/stable/nn.init.html)

### Restarts and Ensembles

* When using random initializations, we can check various initializations
* Then you can report the average model accuracy across all restarts
* Gives an idea of model stability
* **Ensembles** often increase prediction accuracy

### Xavier initialization

* The **magnitude** (scale/size of random numbers) of the random values have a large impact on the learning process
* **Xavier initialization** is widely used to help with this
* $d_{in}$ and $d_{out}$ are the dimensionalities of the weight vectors
 ![[Pasted image 20240129155627.png|500]]

### He initialization
 
* Samples from a gaussian distribution to create initial values
 ![[Pasted image 20240129155829.png|500]]

## Step-wise training
_First train lower, then further layers_

* Freeze parts of network, and only train on the other parts
* Can help minimizing vanishing or exploding gradients, as you are more likely to get useful gradients in the earlier layers
* Can also help learning hierarchical features, by first learning lower layer more low-level representations in the lower layers, then progressively learn more abstract higher layer features
* Can also be used for **transfer learning** [[Week 10 - Dialogue Models#1. Use transfer learning to exploit models on related domains|(from IN4080)]], which means to first train a general purpose model to learn a lot of different things, then fine tuning to custom needs

## Normalization
_Rescales the values to be of a similar scale, often [0,1]_

* Normalization techniques, like **batch normalization**, can be useful to reduce exploding or vanishing gradients


## Regularization
_Used to prevent overfitting by adding a penalty term to loss function_

### L2 Norm
* Also known as **weight decay**, calculates the magnitude of a vectors values
* Can be used for normalization by adding the **L2 Norm** to the loss
* [[Week 5 - Scoring, Term weighting and Vector Space Model#Length normalisation (L2 norm)|From IN4120]]
* $||\vec{x}||_{2}=\sqrt{\sum\limits_{i}x_{i}^2}$

![[Pasted image 20230913105705.png | 350]]

### Dropout
* Very simple and effective regularization
* When training the network, zero out a random set of nodes in each layer (for example 50%)
* Helps by forcing the network to not be too dependent on a few nodes
* ![[Pasted image 20240129164944.png|400]]



## Special architectures

* Special architectures exists to reduce gradient problems
* **LSTM** and **GRU** are both used to reduce this problem


## Optimization algorithms

* Choosing a different optimization algorithm for the weights can help
* Stochastic gradient descent works well, but can be slow to converge
* AdaGrad, Adam, etc. are good alternatives
	* Easy to change in PyTorch:
		![[Pasted image 20240129155301.png|500]]

## Shuffling

* The order in which training examples are presented is important
* To make sure the model does not take the order into consideration, it is recommended to shuffle the training data before each training epoch


## Learning rate

* Tuning learning rate can affect the speed of training and the accuracy
* Large learning rate with prevent convergence, but be faster to train
* Small learning rates take longer to converge, but can be more accurate
* Small learning rate can also be more likely to be stuck in local optima

## Batch training

* The size of each batch is significant and can affect the speed and accuracy
* Large batches are sometimes helpful (depends on task) and can be more computationally efficient than small batches