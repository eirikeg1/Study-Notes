
## VGG architecture
* Deep with small filters
* Dropout

# Regularization
---
## Dropout regularization

* Temporarily remove some neurons from a network for a pass during training
* Regularization technique, used to improve test score on the test set (or other data not used for training)
* Used to make sure the model does not rely too much on specific neurons
* Fraction of neurons active at each iteration $1−p$
	* At **inference**, use the entire network while scaling parameters down by $1-p$
* [[Week 2 - Practicalities and hyper-parameters#Dropout|Dropout in IN5550]]
![[Pasted image 20240219103518.png|350]]
### Formula
* Bernoulli random variables $r_{j}^{[l-1]~Bernoulli(p)}$
* $\circle$ is Hadamard product
![[Pasted image 20240219102543.png|350]]


## Batch Normalization

### Why?
* Prevent small changes to the parameters from amplifying into larger and suboptimal changes in activation in gradients
* Prevents the training from getting struck into the saturated regimes
* Make training more resilient to parameter scale
* Improve generalization

### How
* Activations will have standard deviation $\gamma$ and mean $\beta$ with $\gamma$ and $\beta$ trainable
* Can be added anywhere in your network
* To work well, it usually requires a batch size of 8 at least, better 16 or 32 or more
* In **convolutional layers:** treat each neuron in the same channel in the same way
	* Compute mean and standard deviation for all elements in the feature map of one channel
* Two steps:
	1. Normalize activations of a layer to have zero mean and standard deviation one over elements of a mini-batch
	2. Apply a simple affine transformation on the normalized output $y= \gamma \hat{y}=\beta$

![[Pasted image 20240219111925.png|350]]

### Training time
* update running mean and running variance #toExpand 

### Inference time
* In coding: use `model.eval()` or `model.train(False` at testing time for your network)
* Two steps:
	1. Normalize activations of a layer by the running mean and running variance learnt at training time
	![[Pasted image 20240219112521.png|250]]
	
	2. Apply $y= \hat{x}+b$ with $a,b$ the learnt rescaling parameters

## Group normalization
* Alternative when we cannot us large batch sizes


# Fine tuning
---

* Bad idea to train deep neural networks from scratch unless your data is in the order of hundred thousands+ and you have a lot of compute
* This is because the low level filter, which picks up small patters, in big models are often very powerful and low level features will likely be very similar
* Idea is to start at a good loss, and then optimize to find a close local minima
* Can be useful to reduce overfitting
## How
* Take a deep network and initialize it with weights from a similar task
* Can use [pretrained PyTorch models](https://pytorch.org/docs/stable/torchvision/models.html)
* Retrain it for your classes
* Each layer is optimized for the layer before, therefore you should not remove layers below. Common practice to only train last fully connected layer/s
	* Can be useful to train all the layers if you have a huge dataset, but usually works bad for small datasets

# Models
---
## GoogLeNet

### Idea 1: auxiliary classifiers
* Only done at training time for the loss calculation
* Encourage discrimination at training time only
* Auxiliary output is a separate classification output
* Coss-entropy loss to estimate class probabilities
* Overall loss is a weighted sum of main and aux losses


- ![[Pasted image 20240219103728.png|300]]

### Idea 2: Inception Module
* Convolution layers in parallel with different effective filter sizes
* Next layer can abstract features from different scales simultaneously
* $1\times 1$ convolutions to reduce parameters with large $\#$ filters

* ![[Pasted image 20240219104015.png|350]]

* ![[Pasted image 20240219104709.png|350]]

*  At inference we also take the average over multiple classifiers and massive data augmentation
* Often take the average of for example the top-5 classifiers
* ![[Pasted image 20240219105043.png|350]]

* A $3 \times 1$ convolution followed by a $1 \times 3$ convolution is equivalent to sliding a two layer network with the same receptive field as in a $3 \times3$ convolution
	* $3 \times 3$ is 33% cheaper
	* Reduction of filters geometric sizes comes at a cost of expressiveness
	* In practice not good on early layers, but good on medium
* Each $5 \times5$ is replace by two $3 \times3$
* ![[Pasted image 20240219105603.png|350]]

## ResNets

* Uses **residual connections** (skip connections to layers further down)
	* A linear mapping (instead of identity) whenever number of filters changes to match dimensions
	* Uses **Batch normalization** after every convolution

### Residual connections

* Residual connection with 2 convolutional blocks
* When gradient flows through shortcuts, it reduces [[Week 2 - Practicalities and hyper-parameters#Vanishing gradients|vanishing gradients]]
* In forward pass: if convolution block is not useful, it will be bypassed
	* Learned functions is at least as good as the one without convolutional blocks
* 
* ![[Pasted image 20240219105930.png|250]]
* ![[Pasted image 20240219105748.png|350]]


## DenseNets

* Within a block of same feature map size (_dense block_), each layer contains the feature amps of each the previous layers in the same block, via concatenation of layer maps
* **Growth rate**: $\#$ of newly added output channels in convolutional layer
* In order to stop a too big growth rate, we again use $1 \times1$ convolutions with BN and ReLU before each layer to control the number of channels

![[Pasted image 20240219113541.png|300]]

![[Pasted image 20240219113705.png|350]]
