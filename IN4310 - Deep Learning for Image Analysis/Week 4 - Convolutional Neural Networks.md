
* Lets us use much fewer parameters than **fully connected networks**
* Local pattern detection and translation invariance
* sliding window
* Are often used in image analysis/generation
* Early layers learn simple patterns, learn more complex the deeper we go

# Convolutional Operator (Filters)
---

## Why?

### Fully connected layers with one input channel
_Every node is input to every node in next layer_

* Used in [[Week 2 - Multi-layered Networks and Deep Learning#Feed-forward neural networks|feed forward neural networks]]
* Calculate weighted sum for each parameter
* Here we connect every single output to every single input parameter: very expensive with multiple layers

![[Pasted image 20240212184338.png|400]]

### Focus on local patterns
_Connects neurons sparsely when stacking layers_

* Neighboring pixels tend to be related
* Connect only neighboring neurons in the input

![[Pasted image 20240212184657.png|400]]


## Filters

* Instead of having neurons fully connected, use **filters** (or **kernels**) to find local patterns in the data
* **Filters** are vectors with a set of values. The model uses a sliding window approach to _slide_ over the input data and apply the **dot product** between the input values and the filter
* Learning algorithm learns **Kernel values** through **ERM**
![[Pasted image 20240212184930.png|450]]

## Examples

### Algebraic Properties of (Discrete) Convolution

* Convolution defines a product on a vector (linear) space
* Such space is a commutative associative algebra without identity
* Commutativity $f\cdot{g}=g\cdot{f}$
* Associativity $(f\cdot{g})\cdot{h}=f\cdot{(g\cdot{h})}$
* Distributivity $f\cdot{(g+h)}=(f\cdot{g})+(f\cdot{g})$
* Associativity with scalar multiplication $\alpha (f\cdot{g})=(\alpha{f})\cdot{g}=f\cdot(\alpha{g})$

### 2d convolution example with one input channel

![[Pasted image 20240212190240.png|400]]

![[Pasted image 20240212190305.png|400]]
![[Pasted image 20240212190326.png|400]]
...
![[Pasted image 20240212190459.png|400]]


### 1d convolution example with multiple input channels

* For example, each channel represents the color (one for red, one for green and one for blue)
![[Pasted image 20240212191444.png|400]]


### 1d convolution example with multiple output channel

![[Pasted image 20240212191701.png|400]]

### Filter for extracting horizontal / vertical edges

![[Pasted image 20240212191946.png|400]]

![[Pasted image 20240212192029.png|400]]


### 2d discrete convolution and cross-correlation

* Convolution of a 2d image $x$ and a 2d kernel $K$:
![[Pasted image 20240212192204.png|350]]
* Several neural network libraries implement **cross-correlation** equivalent formulation:
![[Pasted image 20240212192254.png|350]]
* For simplicity, we call both operation **convolution**