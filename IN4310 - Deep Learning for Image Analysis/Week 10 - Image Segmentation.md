![[Pasted image 20240422134318.png]]

# Semantic Segmentation
_Classify every single pixel into it's belonging class_
* Differentiate between classes, but not multiple instances of the same class

## Naïve approach 1: Sliding window
* Slide and find the anchor boxes of each class. Run [[Week 4 - Convolutional Neural Networks#Fully Convolutional Neural Nets (ConvNets and CNNs)|CNN]]s on every anchor box
* Same approach as in [[Week 9 - Object detection]]
* Can work, but is not very popular anymore
* Slow, can be very expensive
* Does not have a global context, for example if the [[Week 4 - Convolutional Neural Networks#Receptive Field (Field of View)|receptive field]] is small and only gets the center patch of fur of the cow, it might not have enough information to differentiate if the fur belongs to a cow or a goat
	* This might not always be needed for all problems
* ![[Pasted image 20240422135359.png|350]]

## Naïve approach 2: CNN without downsampling
* Again, small receptive field can be problematic
* Is more efficient than naive approach 1, but still expensive for large images
* Can't use existing pre-trained networks, as you would need downsampling
![[Pasted image 20240422135942.png|450]]

## Basic sketch for semantic segmentation

* Have large receptive fields (for example by using downsampling) to capture large spatial areas for global context.
	* Feature maps with large receptive field have low resolution
* Use information from early low resolution layers to capture finer details (boundary of the segmentation mask)

## Different problems/challenges
### Capturing global context
_Information from the entire image_
* Downsample feature maps using max/avg [[Week 4 - Convolutional Neural Networks#Pooling|pooling]] or convolution with $\text{stride}>1$
* 


# Instance Segmentation
_Classify the different objects you want into their own class_

# Panoptic Segmentation
_Combination of semantic and instance segmentation, classify every single pixel but differentiate between each object_

