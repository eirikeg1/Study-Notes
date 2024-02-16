
# Feed-forward neural networks
---
_A classical neural network_

* Can, in theory, approximate **any** function given enough neural width and layers and unlimited training data
## Fully-connected

* Feed forward networks are **fully-connected**, meaning that each neuron in the layer $I^n$ is connected to each neuron in the layer $I^{n+1}$
* Mathematically a vector-matrix multiplication $x^{n}\cdot W^{n}=x{{n+1}}$
* Not all neural architectures are not fully connected, but classical **Feed-forward neural networks** are

## Non-linear transformations

* Non-linear transformations are required to get classification boundaries for data which is non-linear
* In a multilayered network we transform the data for each layer
	* Transformations themselves are linear, but followed by a non-linear operation at each layer
* All weights are calculated at the same time, with matrix multiplication
	  $\phi(x)=g(\cdot W')$
	  $\hat{y}=\phi(x)\cdot W$
## Bias

* **Bias** is added trivially to each layer, often except the last one
* Can be used for generalization, to give the model more _freedom_
* Then a neural network can be described as $\hat{y} = g^2(g^{1}(x\cdot W^{1}+b^{1})\cdot W^{3}\cdot b^{2})$
	* $g^{1}$ and $g^2$ are non-linear activation functions


## Parameters

* 

## Popular activation functions
_Activation functions are used to introduce non-linearity in the model_

* [[Week 7 - Neural networks#Activation functions|Different activation functions]]
