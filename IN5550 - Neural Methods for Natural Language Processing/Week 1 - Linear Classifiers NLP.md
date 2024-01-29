
# Relevant notes
---

* [[Week 3 - Classification 2#Linear Classifiers|Linear classifiers from IN4080]]


![[Pasted image 20240124150226.png|700]]


# Linear classifying text
---

## The main classes of NLP tasks are

### Regression
* Returns a scalar
* How positive is $x$ from 1-10
### Classification
* Which of these classes are most relevant to input?
* Can be multi-class, with a lot of different classes
### Ranking
* Rank the input according to $x$
### Structure prediction
* Part of speech tagging, which type of word is this, ...


## Bag of words feature vector

* Can be used in order to classify text
* Explained in [[Week 2 - Classification 2#Bag of words|IN4080 slide]], also check out [[Week 6 - word2vec embeddings#Continuous bag of words|Continous bag of words]]
* Use one-hot encoded vectors, where each index represents a specific word
	* Value can either be the count of that particular words in the document, or a Boolean ( if it appears in document or not)


## Log-linear classification

* [[Week 3 - Classification 2#Logistic regression|Logistic regression from IN4080]]
* If we care about how confident the classifier is about each decision we can map the output in the range [0,1]

### Sigmoid
* This can be done with a function, like for example the **sigmoid function**
	* $\hat{y}= \sigma (f(x)) = \dfrac{1}{1+e^{-(f(x))}}$
	* Results in the _probability_ of the result
* For multi-class cases, log-linear models produce probabilities for all classes, for example $\hat{y}=[0.4,0.1,0.9,0.5]$ $(for$ $k=4)$
* Then choose the class with the highest score

### Softmax
* Often it is more convenient to transform scores into a probability distribution, when dealing with multi-class classification
* $\hat{y}=softmax(xW+b)$
	* $\hat{y}_{[i]} = \frac{e^{z_{[i]}}}{\sum_{j=1}^{K} e^{z_{[j]}}}$


# Training
---

## Loss function
_Function which takes in predicted $\hat{y}$ and gold label $y$, which returns a scalar based on how close $\hat{y}$ is to $y$_

* It can be useful to pose restrictions on the possible $\theta$, in order to not overfit
* As $\theta$ should not be to complex, it should be lean and avoid large weights
* We use learning rate $\lambda$ and regularization term $R(\theta)$ in order to regularize (make a more generalized prediction)
* [[Week 7 - Neural networks#Loss|Loss from 4080]]

### Regression
* Mean Absolute Error
* Mean Squared Error

### Classification
* **Hinge-loss** (max-margin)
	* Binary: $L(\hat{y}, y) = max(0,1-y\cdot \hat{y})$
	* Multi-class $L(\hat{y},y)=max(0,1-(\hat{y}_{[t]}-\hat{y}_{[k]}))$
	* Returns 0 or value of loss
* Log-loss
	* $log(1+ exp(-(\hat{y}_{[t]}-\hat{y}_{[k]})))$
* **Cross-entropy loss**
	* Binary (logistic loss): $-y$ $log(\hat{y})-(1-y)log(1-\hat{y})$
	* Categorical (negative log-likelihood): $-\Sigma y_{[i]} log(\hat{y}_[i])$
	* [[Week 3 - Classification 2#Cross entrophy loss|Notes from IN4080]]

### Ranking
* Ranking loss
* Triplet loss


## Optimizing training (improve loss)

* **Hill climbing algorithm**, make random changes to parameters, if better keep them
* **Gradient based methods** are more popular now

## Gradient based methods
_Uses gradient descent to calculate better parameters during training_

* $\hat{ \theta} = argmin_{\theta}(L( \theta) + \lambda R(\theta))$
* Steps
	1. compute the loss
	2. compute gradient of $\theta$ parameters with respect to the loss
	3. _(Gradient is now a collection of partial derivatives, one for each parameter of $\theta$)
	4. Move parameters in the opposite direction (to decrease the loss)
	5. Repear untill optimum is ound, or end clause

### Training methods

#### Stochastic gradient descent
* Update weights after every training sample (samples of one prediction)
* Can lead to quick convergence, but can be less stable and computationally expensive
* [[Week 3 - Classification 2#Stochastic gradient descent|From IN4080]]

#### Batch training
* Split training set into $k$ batches. Update weights after each batch, based on total loss
* More often used


