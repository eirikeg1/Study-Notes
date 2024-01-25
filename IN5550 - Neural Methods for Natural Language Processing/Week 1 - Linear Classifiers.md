
# Relevant notes
---

* [[Week 3 - Classification 2#Linear Classifiers|Linear classifiers from IN4080]]


![[Pasted image 20240124150226.png|700]]


# Linear classifying text
---

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
	* 



