#todo 

## Classifying a single object

* Draw a bounding box around the object

# Two object detection approaches
---
## One-stage detector

* Pass (process) the image through a Neural Network
* On the final feature map(s) of the network:
	* Slide a window
	* For each window location, predict an object class and a bounding box for each _anchor_ (also called default box or prior), i.e. adjust the anchor
	
![[Pasted image 20240419121223.png|300]]


### One stage anchor-free detectors
* Same as one-stage detectors, but instead of adjusting anchor directly predict:
	* Top-left and bottom right corners
	* And/or the center of objects

## Two-stage detector

### Stage 1
* Generate multiple candidates (bounding boxes) all over the images, typically makes use of **anchors**
	* **Selective search**, Reason Proposal Network
* Throw away the candidates without an object

### Stage 2
* Process each candidate independently
* Assign a category (class) to each candidate and adjust its bounding box

![[Pasted image 20240419121215.png|300]]

# Models
---
## R-CNN
_Does not run the whole image through a CNN at once, but detects smaller areas and runs smaller CNNs on the local area._
### Steps
1. Propose **ROI**s (Region Of Interest)
	* Can be through for example selective image search (is run on CPU, pretty slow)
2. Run [[Chapter 1 - Introduction#Convolutional Neural Networks|CNN]] on each of the candidates

![[Pasted image 20240419122548.png|350]]

## Fast R-CNN
_Instead of doing a CNN on each candidate we run the image through a ConvNet_

![[Pasted image 20240419122818.png|350]]

## Faster R-CNN

1. Start with a Pre-trained CNN to get feature maps
2. Run through Region Proposal Network to get proposals using anchor boxes
3. Classify candidates as in **Fast R-CNN**
![[Pasted image 20240419123036.png|350]]

# Generating candidates using anchors

## Receptive field for candidates
_If something is determined to be a object at an anchor, the model actually looks at the whole context within its receptive field_
* [[Week 4 - Convolutional Neural Networks#Receptive Field (Field of View)|Receptive field]] decides if it is classified as an object
* If the receptive field is too big, it is very hard to determine where the object actually is

## Anchor boxes
_Allows multiple objects to have the same center location_
![[Pasted image 20240419124724.png|400]]


# Different sized objects
---
* Anchors of varying sizes help, but anchors at a location are limited by that location's receptive field size

## Single shot Multibox Detector (SSD)

* Works well in practice, but can be improved
* Is a [[#One-stage detector]] until around halfway
*  

![[Pasted image 20240419125340.png|350]]


## Feature Pyramid Network (FPN)

* Originally proposed as a [[#Two-stage detector]]
* The deeper in the layers you go, the semantically stronger the features get
	* Only larger anchor boxes benefit from this, due to larger receptive field
* You copy an image and upscale it for each layer, 

 ![[Pasted image 20240419150649.png|350]]

# Problems
---
## Overlapping predictions
_The model might detect the same object multiple times_

### Non-max suppression

 * Remove all boxes having no $c_{1}, c_{2}, \dots , c_{x}$
* Lower score of bounding boxes based on overlap
* ![[Pasted image 20240318112538.png|300]]

	![[Pasted image 20240318111759.png|300]]
	![[Pasted image 20240318111814.png|300]]


### Matching anchors with ground truth boxes
	![[Pasted image 20240318113323.png|300]]

### Too many background predictions

#### Hard Negative Mining
_Select only the most difficult background patches_
* *Most difficult* based on loss
* **OHEM**, Online Hard Example Mining


#### Focal loss
_Change loss function to downscale importance of highly certain background patches_

* Control loss with $\gamma$
* Optionally add more weights to the non-background patches
	* $\alpha$ factor often mentioned in conjunction with focal loss
	
	![[Pasted image 20240318114041.png|300]]

# Anchor-free approaches
_No pre-defined set of anchor boxes_
#NotImportant
* **CenterNet**, **FCOS**, transformer-based networks #toLink
* Instead of anchor boxes, output:
	* class
	* (left, right, top, bottom)
	* center or "center-ness"
* ![[Pasted image 20240318114520.png|300]]


# Performance and evaluation metrics
---

* [[Week 7 - Performance estimation and generalization#Mean average precision (mAP)|mAP]]
	* You add **IUO** thresholds #toLink
* [[Week 2 - Classification 2#Precision and recall|Precision and Recall]]
* 