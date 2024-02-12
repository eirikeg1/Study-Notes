
* Lets us use much fewer parameters than **fully connected networks**
* Local pattern detection and translation invariance
* sliding window
* Are often used in image analysis/generation
* Early layers learn simple patterns, learn more complex the deeper we go

# Convolutional Operator (Filters)
---

* **Convolution** is a series of dot products
* Dot product between filter and a window-view of input tensor
* Window is sliding for 1d and 2d convolutions along 1 or 2 dimensions
* The number of **filters** (**kernels**) or channels is represented as $\#$
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
* Therefore it might not be necessary and just a lot of unnecessary overhead to to everything else as context for every single input/output
* Each convolution layer detects localized patterns over all input tensor

![[Pasted image 20240212184657.png|400]]

### Less parameters and parameter sharing

* **Locally connected**: Suppose each output neuron takes input from a patch of 5 neighbors
* convolutions have a small $\#$ parameter, independent of input and output size in the sliding dimension ($\#$ output channels (filters) matters)

### Translation Invariance
_Property of  ML models where predictions are invariant or do not change, when the input is translated or moved around_

* Detection is global for fully connected (no translation invariance), localized for convolutions 
* Detect similar patterns in different sizes/scales
* Detect similar patterns from different view angles
* Detect deformations of the same pattern/object
* Detect different types in the same class

## Week 4 Why conv.? #Todo
## Filters

* Instead of having neurons fully connected, use **filters** (or **kernels**) to find local patterns in the data
* **Filters** are vectors with a set of values. The model uses a sliding window approach to _slide_ over the input data and apply the **dot product** between the input values and the filter
* Learning algorithm learns **Kernel values** through **ERM**
![[Pasted image 20240212184930.png|450]]


### Algebraic Properties of (Discrete) Convolution

* Convolution defines a product on a vector (linear) space
* Such space is a commutative associative algebra **without identity**
* **Commutativity**: $f\cdot{g}=g\cdot{f}$
* **Associativity**: $(f\cdot{g})\cdot{h}=f\cdot{(g\cdot{h})}$
* **Distributivity**: $f\cdot{(g+h)}=(f\cdot{g})+(f\cdot{g})$
* **Associativity with scalar multiplication**: $\alpha (f\cdot{g})=(\alpha{f})\cdot{g}=f\cdot(\alpha{g})$

### 2d discrete convolution and cross-correlation

* Convolution of a 2d image $x$ and a 2d kernel $K$:
![[Pasted image 20240212192204.png|350]]
* Several neural network libraries implement **cross-correlation** equivalent formulation:
![[Pasted image 20240212192254.png|350]]
* For simplicity, we call both operations **convolutions**
* We learn the kernel values through **Empirical Risk Minimization** (**ERM**) #toLink


### Convolution with multiple channels

* Convolution kernel has additional dimensions for input and output channels
* $C_{i} \#$ input channels in the feature map to be processed
* $C_{o}\#$ output channels
* We use tensor notation with brackets
* Let $r=1,\cdots ,C_o$
![[Pasted image 20240212203012.png|500]]

## Padding


![[Pasted image 20240212195246.png|250]]

* To keep output size unchanged compared to input, one can pad the image
* Most common in deep learning: pad with 0s (**zero padding**)
* Expand input image with another fixed value, e.g. mean pixel value
* Use value of nearest pixel (replicate padding)
* Use mirror-reflected indexing (reflect padding)

### Output size

* For $M\times N$ input and $k\times k$ filter

**For sizes:**
* **Valid or reduced**: Only positions where the filter fits inside input
	* Output will have smaller size than input $(M-k+1)\times (N-k+1)$
* **Same**: Positions where the filter center is inside input
	* Output will be the same size as input
* **Full**: All positions where the filter and input overlap
	* Output will have larger size than input $(M+k-1)\times (N+k-1)$


## Convolution Intuition

* Control $\#$ parameters limited relative to training set size to generalize well
* Better off stacking simple functions in depth and many layers than learning complex functions in one layer
* Convolution output at one fixed input region is an inner product between kernel weights and the region
* Slide the kernel over the input tensor and apply the inner product over many windows
* Apply the same kernel across all locations for computing inner products
* Share the parameters to be learned

## Stacking layers

* At each convolutional layer, apply a set of local filters
* Stack multiple small filters instead of using few large filters
* Remember that convolution is associative
* Requires much less parameters with more smaller filters:
	* Two $3\times 3$ filter has 18 parameters, one $5\times 5$ has 25 parameters
	* Three $3\times 3$ filters have 27 parameters, one $7\times 7$ filter has 49 parameters
	* Four $3\times 3$ filters has 36 parameters, one $9\times 9$ filter has 81 parameters
* Focus on very local image attributes int he first convolutional layers
* Look for gradually more complex patterns in deeper layers


## Examples

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



