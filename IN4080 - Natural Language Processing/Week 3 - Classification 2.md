
# Regularization
---
_Technique which makes the features to a similar size, used to reduce overfitting_

* Reduces overfitting by penalizing large weights, so no single feature/weight overrides the others
* Can be specified with the _penalty_ and _C_ parameters in Scikit-learn
* L1 regularization:
	![[Pasted image 20230906160625.png | 350]]
* L2 regularization:
	![[Pasted image 20230906160659.png | 350]]

# Linear Classifiers
---
* Linear decision boundary 
	![[Pasted image 20230905145321.png | 350]]
* When more than two dimensions the line becomes a hyper-plane:
	![[Pasted image 20230905145430.png | 350]]
* Different models compared:
	![[Pasted image 20230912143124.png  | 350]]

# Generative vs Discriminative classifiers

* Online training (update after every single instance, for example in stochastic gradient descent)
* 
## Discriminative:
* Tries to find a straight line by trying to find a straight line as a decision boundary
* If a new class the hyperplane is changed (has to be retrained)

## Generative
* Tries to independently build models to explain what each class look like
* With new class just calculate the model for the new class and keep the old ones
* Solve harder problem than just classification, not as useful if this everything you want

#### Underlying idea:
 * For each document 𝑥: 
	 * Determine a class label according to 𝑃෠(𝑦) 
	 * Generate word counts according to the 𝑃෠(𝑥𝑖 |𝑦) 
 * How likely is it that the observed document 𝑥 (i.e. its bag of words) with label 𝑦 has been generated from the distributions 𝑃?


![[Pasted image 20230912142656.png | 350]]

# Perceptron
---

* Does not use probabilities
* Is a linear classifier
* Still uses Bag-of-words representations
* Associates each feature *f_i* with a weight *w_i*
	* Feature values change with instance
	* Weight value change with class
* Smoothing not important	

## Scoring function
_(sum weight * feature)_
* Uses steppe function (sums the weights multiplied with the values and chooses above or below threshhold)
* weight and features represented as vectors:
	 ![[Pasted image 20230905143113.png | 350]]
* Scoring function represented as dot product:
	 ![[Pasted image 20230905143143.png | 350]]
* Normal representation:
	 ![[Pasted image 20230905142253.png | 350]]

# Training:
* Take one instance 𝑥 of the training set 
* Predict a label 𝑦 using the current model 
* If the prediction is correct, nothing happens 
* If the prediction is wrong, modify the parameters of the model 
* Continue untill stop conditions 


### Updating weights

* If prediction is correct nothing happens
* If prediction is wrong:
	* Add the value of the feature value to the weight in the correct class
		![[Pasted image 20230905144249.png | 350]]
	* Remove the value of the feature value to the weight in the correct class
		 ![[Pasted image 20230905144838.png | 350]]

### Stop conditions
* Number of epochs (not great)
* When no updates for a full epoch (model has converged)
* When number of updates per epoch is below predefined threshold 
	* Not all models converges as they have to be linearly separable

# Implementation
![[Pasted image 20230905144423.png | 750]]


# Logistic regression
---
_Works same way as The Perceptron, but uses a logistics function instead of a step function_

* Gives probabilities instead of scores, can be more useful
* Probabilities are not independent, adding new class requires retraining everything
* Is pretty much always better than Naïve Bayes on **training** data. Can have a problem with overfitting
* Only has one weight vector
* Scoring function (Logistic/sigmoid function):
	  ![[Pasted image 20230905154115.png | 350]]
* Use softmax function to get probabilities:
	![[Pasted image 20230905151957.png | 350]]

# Training
### Updating weights
* Lambda means learning rate:
	  ![[Pasted image 20230905152701.png | 350]]
* In contrast to the perceptron it updates the weights of not only the gold and predicted classes. It changes all weights based on the predicted probability

### When to stop training
* Predefined number of epochs
* Overall probability of training data
* When the classification performance on the validation set stops improving



# Variants
### Regression point of view (1 input feature)
	![[Pasted image 20230905154248.png | 350]]

### Classification point of view (2 input features)
	![[Pasted image 20230905154315.png | 350]]


# Learning

* The measure for how well we're doing on dataset *D* the probability of the dataset given the weight vector:
	![[Pasted image 20230905154645.png | 350]]
* By convention we take the logarithm of this probability, which is called the **Objective**:
	![[Pasted image 20230905154731.png | 350]]
* The model is good if objective is large

#### Cross entrophy loss

![[Pasted image 20230905154902.png | 350]]
* Rather than maximizing an objective, learning process is usually formalizes as minimizing the loss:
* Gives a convex loss, allows for gradient descent
* Finding the minimum of L(w):
	1. Pick random value
	2. Evaluate L'(w)
	3. If L'(w) = 0 it is correct
	4. If L'(w) < 0 increase weight
	5. If L'(w) > 0 decrease weight
* **Gradient descent:**
	![[Pasted image 20230905155554.png | 350]]

# Different learning strategies

## Batch training
1. Calculate loss for whole training set
	![[Pasted image 20230905155743.png | 350]]
2. Make one move with gradient descent
3. Repeat

## Stochastic gradient descent
1. Pick one item from training data
2. Calculate loss for this item
3. Move in the direction of the gradient for this item

* Fast but unstable

## Minibatch training
1. Sample a small number of instances from training data
2. Calculate the loss for this subset
3. Make one move with gradient descent

* Good compromise between speed and stability
* Standard approach used with neural networks


# Inductive bias
---
## Restrictive bias
* Refers to the assumptions that limit the set of functions that the algorithm can learn

## Preferential Bias
* Preferential bias refers to the assumptions that make some functions more likely to be learned than others
