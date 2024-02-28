

# BackPropagation
---

## Gradients

* The surface of hyperplane has slopes
* Gradient contains information about all directional derivatives
* ![[Pasted image 20240226102340.png|350]]

### Directional derivative
_How much a function grows along a direction under an infinitely small step_

* Formula:
	* ![[Pasted image 20240226102550.png|200]]
* If function is differential, the directional derivative in x along v is the inner product of gradient and direction:
	* ![[Pasted image 20240226102610.png|200]]


### Gradients through partial derivatives

* Let $e_i$ be a vector with all elements equal to $0$, except the $i$-th, which is 1
* ![[Pasted image 20240226102859.png|400]]
* Then: ![[Pasted image 20240226102913.png|300]]
* Let $v=[v_{1} \dots v_n]^T$. We note: ![[Pasted image 20240226103104.png|300]]


## BackPropagation for Neural Networks
---
![[Pasted image 20240226103153.png|300]]
 
* Network: ![[Pasted image 20240226103204.png|300]]
* Concatenate all outputs of $a_{k}^{[l]}$ of layer $l$ and apply $g$ element-wise
	* ![[Pasted image 20240226103338.png|300]]
* $W^{[l]}a^{[l-1]}$ is a matrix-vector multiplication

### Forward direction

* Forward formula for layer $l$: ![[Pasted image 20240226103510.png|200]]
* Whole formula: ![[Pasted image 20240226103529.png|400]]



### ERM with cross-entropy loss

* ![[Pasted image 20240226104036.png|300]]
* Model's predicted probabilities $\hat{y}_{n}\in [0,1]^{n_{y}}$
* ![[Pasted image 20240226104018.png|350]]
*  ![[Pasted image 20240226104001.png| 300]]


### Gradient descent for ERM #toExpand 

* ![[Pasted image 20240226104142.png|300]]
* Complexity $O(d)$
* Initialize $\theta_0$
* For $t=0,1,2,\dots$
	* ![[Pasted image 20240226104221.png|350]]
* Gradient descent update rule: ![[Pasted image 20240226104250.png|300]]
* Stochastic gradient descent:
	* ![[Pasted image 20240226104407.png|300]]
* For simplicity, drop iteration $k$ 

### Chain rule



# Stochastic Gradient Descent
---

