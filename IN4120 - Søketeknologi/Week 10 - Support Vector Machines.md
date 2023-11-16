
# Embeddings
* Dimensions could be the words/tokens,  or encoded by neural network (words are points)

# Support Vector Machines
---
* For tasks when finding a separating hyperplane, a **Support Vector machine** finds an optimal solution
* Maximizes the margin around the separating hyperplane
* Can be fully specified by a subset if training samples (the **support vectors**)
* Widely considered most successful current text classification method
* ![[Pasted image 20231018104850.png | 250]] ![[Pasted image 20231018105321.png | 250]]


# Linear SVM
#toExpand 
## Formalization
#toExpand 
* $w$: Decision hyperplane normal vector
* Classifyer: ![[Pasted image 20231018105555.png | 350]]
* Functional Margin of $x_i$: ![[Pasted image 20231018105637.png | 350]]


## Geometric margin
#toExpand 

* Distance from separator: ![[Pasted image 20231018105736.png | 250]]

# Linear SVM Mathematically
* Can be used to formulate quadratic optimisation problems:
* ![[Pasted image 20231018110100.png | 350]]


## Soft margin classification

* Decision boundaries where we allow som mistakes
* Good if data is not linearly separable
* Slack variables $ξ_i$ can be added to allow misclassification of difficult or noisy examples
* ![[Pasted image 20231018112128.png | 350]]
* ![[Pasted image 20231018111941.png | 350]]



# Non-linear SVMs

* uses kernel functions to map low dimensity data to higher dimensional plane, to make a decision boundary easier #Maybe 
* ![[Pasted image 20231018113201.png | 700]]

### Common Kernels
* Linear Kernels
* Polynomial kernels
	* 
* Radial basis function (infinite dimensional space)
	* In theory infinite dimensions #Maybe 
	* Usually not very useful on text classification
	* ![[Pasted image 20231018113410.png | 350]]



# Data
#toExpand 

### To little data
* High bias is good
* Naive bayes

### A lot of data
* Good in theory for accurate classification
* expensive and time consuming
* **SVM**s and **kNN**s are impractical 


### Tweaking performance
* **Upweighting**
	* Weighting different contributions from different documents
* **Different techniques for zone**
	* Different training sets for title/body #Maybe 
	* 
* Stemming, lowercasing?
	* Sometimes useful, not always
* Figures of merit
* Concept Drift
	* Categories change over time
	* "President of United States" -> changes over time
	* Simple models like Naive Bayes is favored
	* Feature selection can be bad in protecting against concept drifts 


## Pair wise learning
* Ai to classify instance pairs as correctly ranked or incorrectly ranked
* 