
# Internal testing
---
* Split into train, validation and test set

## Validation by resampling

* Instead of a fixed validation set, make multiple val subsets
* More effective
* Evaluating modeling choices multiple times gives better results

### K-fold Cross validation
* [[Week 2 - Classification 2#K-fold cross-validation|K-fold cross validation]]
* Estimates are less influenced by one particular training
* Estimates are less influenced by one particular validation subset
* Can be expensive

### Bootstrapping
* Sample with replacement from non-test data to obtain train subset
* Train using train subsets (with duplicates) #toExpand 


## Subset sizes

* 70, 15, 15 is normal
* Size of test subsets should be considered in relation to the uncertainty of results estimates (based on classes, or if you expect difference of <1%)

### Scaling laws
* Relation between performance and size of training data appear to be on log-log scale
* Therefore performance gained from increasing is initially very high, but gains slower after a point

# External testing
---

## Representability

* Make sure the data does not contain unexpected patterns
* Use a variety of data from different environments
* Lack of representability can lead to racism or stereotyping
	* Example: Cancer detection triggered by tattoos (if you have an unbalanced dataset)

### External datasets
* Use a different, external, dataset to evaluate after, to check generalization
* Becoming more common
* Pre-specification of external test is rarely reported
	* Except in clinical trial studies where pre-specification is required



# Facilitating generalization
---

## Control networks capacity

* Reduce parameters
	* Stack more convolutional layers with small kernel sizes
	* Reduce width (number of channels in convolutions)
* Dropout
* Weight decay


## Facilitate learning

* Residual connections
* Batch normalization
* Transfer learning
* Learning rate schedule


## Image specific normalization
* Aims for making different images more similar
* Calculate mean and standard deviation of whole dataset, then divide by the channel wise standard deviation


## Data augmentation #toLink 
* Color augmentation
* Stain normalization
* Cycle-GAN


## Normalization
* Normalize images of over average standard deviation over whole training set
* 
  
### Macenko normalization
* Use source and target image to combine into a new one
* Take stain from source and add it to target


### Cycle-GAN
* Training data is one image, target image is what you want to use
* Gradually make the training image more and more like target image during training
* Can be expensive


### Distortion
* Can be used to increase dataset
* Trade-off between facilitating the learning of relations that generalize well beyond the development dataset and not occluding relevant information for the prediction task


# Performance metrics
---

* Should be tailored to intended application
* If end user of model shall only use the classifications and not continuous prediction score, the performance metrics should be based on the classifications only
* Multiple metrics might be helpful
* Can sometimes lead to overfitting if too specific


## Confusion matrix
* Matrix with scores of predictions and target for $x$ and $y$
* Useful in object detection
	* False positive if you detect something wrong

## Precision and recall
* Can be called specificity and sensitivity #Maybe
* [[Week 2 - Classification 2#Precision and recall|IN4080: Precision and recall]]
* [[Week 1 - Inverted indices#Precision and Recall|IN4120: Precision and recall]]
* $prec=\dfrac{TP}{TP+FP}$

* $rec=\dfrac{TP}{TP+FN}$


### Precision recall curve

* Precision is increasing, recall is decreasing
* Perfect classifier has curve which goes first straight forward, then right down
* Random classifier curves downwards gradually

| Prediction | Class |
| ---------- | ----- |
| $0.1$      | 0     |
| $0.2$      | 1     |
| $0.3$      | 0     |
| $0.6$      | 1     |
| $0.9$      | 1     |
| $1$        | 1     |


| Prediction | Precision             | Recall                |
| ---------- | --------------------- | --------------------- |
| $0.1$      | $\dfrac{3}{3+2}=0.6$  | $\dfrac{3}{3+0}=1$    |
| $0.2$      | $\dfrac{3}{3+1}=0.75$ | $\dfrac{3}{3+0}=1$    |
| $0.3$      | $\dfrac{2}{2+1}=0.67$ | $\dfrac{2}{2+1}=0.67$ |
| $0.6$      | $\dfrac{2}{2+1}=1$    | $\dfrac{2}{2+1}=0.67$ |
| $0.9$      | $\dfrac{2}{3+2}=1$    | $\dfrac{1}{1+2}=0.33$ |
| $1$        | $\dfrac{0}{0}=1$      | $\dfrac{0}{0+3}=0$    |

## Average Precision (AP)
* Alternative to compute AP
* [[Week 7 - Evaluation#Precision@K (P@K)|IN4120 Precision@k]]
* compute prediction scores for each sample in evaluation set
* Sort samples by their scores in descending order
* Calculate $AP$


## Mean average precision (mAP)
* If multiple classes, average precision can be calculated per class
* Arithmetic mean 


## ROC curves

* Graph mapping $sensitivity$ over $1-specificity$

## Area under the curve (AUC)
* Create al possible pairs with one element chosen from the positive class and one from the negative class
* Can be shown that AUROC is the proportion of pairs where the prediction score of positive class is larger of pre
* #NotImportant 

## AP and AUROC
* Always have multiple metrics
* #toExpand 

## Balanced Accuracy

## Bootstrap confidence interval
* 






# Visualizing filters
---

* Start with random image
* Run features to one neuron you want to visualize
* Calculate the gradient in neuron
* Update image (only) to maximize the filter
* Results in visualization what the features the filter maximizes




