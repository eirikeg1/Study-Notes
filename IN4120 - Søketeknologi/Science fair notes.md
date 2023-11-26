# Support vector machines

* Can be used for classification and regression
* Finds a hyperplane that best separates the data into different classes
* Creates two supporting vectors, where data in training data can be misclassified
* 
* Loosely:
	1. Map data to higher dimensity
	2. Train classifier on high dimensity data
	3. When classifying unknown points, translate it to higher dimension and use that decision boundary

## Support vector classifiers
* Primary goal is to find the optimal hyperplane that separates data into different classes while maximising margin

## Kernel functions
* Maps low dimensity data to higher dimensity data
* Does not actually transform the data, does calculations as if they are in a higher dimension
	* Uses dot product calculations on points to capture the relationship/similarity between the points

### Polynomial kernel functions
* computes relationships between each pair of observations in $d$ dimensions
	* Is used to find a decision boundary
	* Is important to find a good value for $d$
		* Can be done with cross validation
*  $K(x,y)=(x⋅y+c)^d$
* K(x,y) = (x⋅y+c)^d
	* $x$ and $y$ is the input pair
	* $c$ (constant) and $d$ (num of dimensions) is determined using cross validation
	* Role of $d$ is to control the level of non-linearity in the mapping
		* High $d$ can lead to overfitting
	* Role of $c$ is to shift decision boundary and regularization
		* Controls the trade off between a smooth decision boundary and classifying training points better
	* 

### Radial Kernel
* In theory up to infinite dimensions
* Weights points similarly to nearest neighbour algorithm, useful for clustered datasets
* $K(x,y)=exp(−γ∥x−y∥^2)$
* $K(x,y) = e^{-γ∥x-y∥^2}$


### Radial or Polynomial kernel?
* 
