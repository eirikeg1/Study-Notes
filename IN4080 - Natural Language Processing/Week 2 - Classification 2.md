
**Main NLP tasks**
*  Hate speech detection 
*  Sentiment analysis 
*  Language identification 
*  Syntactic analysis 
*  Part-of-speech tagging

# Supervised classification
---
![[Pasted image 20230829143419.png | 500]]

**Focus areas today:**
* Feature extractor: **bag of words**
* Machine learning algorithm: **Naïve Bayes**

## Dataset splitting
* Training data - for training
* Test data - for test accuracy of a model
* Validation set - to compare models

**Common splits:**
* 80% training, 10% validation, 10% test 
* 80% training, 20% validation, test from different source
* Shuffle before splitting?
	* Good to prevent ordered data
	* But can ruin data which for example is ordered by time
	* Maybe some entries are underrepresented, maybe not only have them in validation

## How to prevent too little data:
_Techniques to assess performance of model and estimating it's generalization ability on new, unseen data_

#### K-fold cross-validation
_Train K models with different parts held out for validation_

* Average validation scores
* After this retrain one model with both validation and training and test with test set

![[Pasted image 20230829145243.png | 500]]
 

#### Leave-one-out cross-validation
* Train _k_ models and split training data into _k_ sets. Train each model on the data in all training sets except it's own (the same _k_). When evaluating use the respective dataset.
* Average validation scores

# Evaluation measures
---
## Automatic evaluation
* Assume that the validation and test sets are labeled 
* Hide the labels, let the model predict new labels, and compare the two 
* For each instance, we have a gold label and a predicted label

## Accuracy
_Proportion of matching labels (gold label = predicted label)_

* Can be misleading if the gold data is not evenly distributed (in example below a model which always classifies no is ~92%)

![[Pasted image 20230829145946.png | 500]]

## Contingency table (confusion matrix)

![[Pasted image 20230829151741.png | 500]]

## Precision and recall

**Precision** 
* How many of the accurate predictions did we find?
* true positives / (true positives + false positives)
* 
**Recall**
* How accurate predictions
* true positives / (true positives + false negatives)

![[Pasted image 20230829151827.png | 500]]

### F-measure
_Combines precision and recall into one value_ as a harmonic mean

![[Pasted image 20230829152726.png | 250]]

### Multi-class
_Calculate the accuracy and recall for each class/label, then calculate the average_

**Micro average or macro average**
![[Pasted image 20230829152400.png | 500]]


# Naïve Bayes
---
* Probabilistic classifier
* Multi-class
* Often uses batch training
* Each probability for a class is independent. This means that if you later add a new class you can just calculate the class probability and use the current probabilities for the other classes
# Variants:

**Multinomial Naïve Bayes**
* Uses count-based bags of words (or weighted count-based BOWs)
* Multinomial distribution = probability distribution over vectors of non-negative counts

**Binary Naive Bayes** or **Bernoulli Naïve Bayes**
* Uses binary counts (1 if feature if present or 0 i absent)
* **Bernoulli** tracks if the word is both present but also not present. It checks if it is in the _vocabulary_ (all word types) #toExpand
![[Pasted image 20230829160052.png | 500]]

# Bayesian inference
_Convert normal prediction formula to Bayes' theorem_

* Compute the probability of a document given a label, not the other way around
* All $x_i$ are conditionally independent given the class

**Full prediction function:**
_Multiply the prediction for every word_
![[Pasted image 20230829154021.png | 500]]

**Traditional prediction function:**
![[Pasted image 20230829153259.png | 250]]

**Bayes theorem:**
![[Pasted image 20230829153230.png | 250]]

**Final argmax**
![[Pasted image 20230829153434.png | 250]]


# Bag of words
_Reduces a document to the frequency distribution of it's words_

* Translate word to frequency when using numeric models
* Using this the word order is not important
* Simplifying assumption: a word is equally likely in all positions.
* Each _x_i_ corresponds to a word:
![[Pasted image 20230829153808.png | 250]]

# Training

**Maximum likelihood estimation:**
![[Pasted image 20230829154512.png | 500]]


# Smoothing
_To prevent the probability of going to 0 if a word is not present by adding pseudo counts (adding alpha value)_

**Additive smoothing** or **Lidstone smoothing**
![[Pasted image 20230829155055.png | 500]]

**Add-one / Laplace smoothing:**
![[Pasted image 20230829155209.png | 500]]


# Computing in log space
_Used to prevent underflow problem (computers can't represent very small numbers)_

* Logarithms transforms big positive numbers to small positive numbers and numbers between 0 and 1 into big negative numbers
* Order is preserved: if a>b then log(a) > log(b)

New prediction function:
![[Pasted image 20230829155705.png | 500]]







