#todo 



# Problems
---


## Overlapping predictions
_The model might detect the same object multiple times_

* 

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