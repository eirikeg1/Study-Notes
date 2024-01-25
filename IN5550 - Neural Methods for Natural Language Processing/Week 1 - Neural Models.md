
# Linear models vs neural models
---

## Linear classifiers
* Efficient and effective
* Interpretable to a degree (you can find the most important features by looking at the weights)
* Can be used on their own (often enough in practice), or as building blocks for non-linear neural classifiers
* Can unfortunately only work on linearly separable datasets
	* Does not work on _the x-or problem_:
![[Pasted image 20240125153220.png|250]]


## Transforming the input

* It is possible to transform the input of non-linearly separable problems into linearly separable problems
* For example $\phi (x_1,x_2)=[x_1+x_2,x_{1}\times x_2]$
* This example does not work for all problems

### Support Vector Machines

* Maps the dataset into a higher-dimensional space, making it even more difficult to choose $\phi$ manually
* Scale linearly in time on the size of training data (slow)
* [[Week 10 - Support Vector Machines#Support Vector Machines|SVM from IN4120]]
* Does not actually create a new vector space, as explained in: [[Science fair notes#Kernel functions|Kernel functions from IN4120]]

## Neural methods

* Leaves it to the algorithm to train a suitable representation mapping function
* Simple **multi-layer perceptron**:
	*   $\phi (x) = g(xW'+b')$
		$\hat{y}=\phi (x)W+b$
* $g$ is a non-linear activation function, and $W',b'$ are its trainable parameters
	* [[Week 7 - Neural networks#Activation functions|Various activation functions]]

### Perceptron with 2 hidden layers
* Activation function on each node
* Each connection has a weight
![[Pasted image 20240125155108.png|400]]