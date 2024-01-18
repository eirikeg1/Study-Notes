
# Standing queries

* Hand written text classifiers
* Path from IR to text classification
	* You have info to monitor
	* want to rerun appropriate query periodically to find new items on topic
	* You get sent new docs


# Classification
---

## Manual classification

* Very inefficient
* Accurate when done by experts

## Hand coded rule based

* Vendors provide _IDE_ for writing rules
* Used in government/enterprise
* Can be very accurate if a rule has been carefully refined over time by a subject expert
* Expensive to build and maintain rules


# Supervised learning
---

* Machine learning with target labels
* We will look at a **Bag of Words** approach
	* Does not look at ordering, only presence and word count. 
	* Only word features
* Uses features, which is the input data

## Feature selection
* Reducing features is more cost effective and can improv generalisation
* Could just use most common terms
## Evaluation
* Must be done on test data, therefore we split into training, test and validation
	* val set used during training
* Precision, recall, F1
### K-fold cross validation
* Split dataset into k equal parts, train a model on each of these parts
### Confusion matrix
* 

### Add thresholds for each classification result

* Plot results on an **ROC-curve**
* ![[Pasted image 20231004120655.png | 350]]
* Create a line (curve) through points
* If line is below curve ignore it #Maybe 