
# What is it?

* Neural networks are just differentiable parameterized functions, which we use gradient-based optimization techniques on
* In order to do this we have to calculate the gradient
* We can use **reverse-mode automatic differentiation** (i.e. **back-propagation**) to automatically calculate the gradients
* A computational graph is an abstraction, which represents the process of computing mathematical expressions in order to construct arbitrary deep and complex network architectures


# How

* Computation is broken down into separate operations
* Each operation and variable is a node in a graph
* ![[Pasted image 20240130135835.png|400]]

Neural networks are trained in two main stages:
1. **Forward pass** (compute prediction for given inputs)
	* Go over all nodes sequentially
	* Produce output up to the final scalar loss-node
2. **Backwards pass** (compute gradients with respect to loss)
	* Loss functions are as a rule the same as with linear models
	* cross-entropy is arguably the dominant one: $L(\hat{y}, y)=-log(\hat{y})-(1-y)log(1-\hat{y})$
	* **NB**: The output should be squashed by sigmoid or like