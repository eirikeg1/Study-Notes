![[Pasted image 20240422134318.png]]

# Semantic Segmentation
---
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
![[Pasted image 20240422135942.png]]

## Basic sketch for semantic segmentation

* Have large receptive fields (for example by using downsampling) to capture large spatial areas for global context.
	* Feature maps with large receptive field have low resolution
* Use information from early low resolution layers to capture finer details (boundary of the segmentation mask)


## Capturing global context
_Information from the entire image_
* Downsample feature maps using max/avg [[Week 4 - Convolutional Neural Networks#Pooling|pooling]] or convolution with $\text{stride}>1$
* Can also be solved by using **dilated convolutions** (also called **atrous convolution**)

### Solution 1: Encoder-Decoder architecture
1. Encode the input to a vector using only convolutions
2. Upsample the encoded vector to image-size resolution
	* Might be better to do this gradually using more parameters

	![[Pasted image 20240422145116.png]]

### Dilated- / Atrous convolution
* Dilation rate $r$, input $x$, output $y$ and kernel $w$
* Standard convolution is a special case of atrous convolution with $r=1$
* Atrous convolution replaces downsampling layers. Double the dilation rate to replace the downsampling layer
* If you use $\text{stride}=2$ with the dilation below ($1$), every other value will be skipped
* ![[Pasted image 20240422160510.png|300]]
* ![[Pasted image 20240422160341.png|450]]

## Upsampling features
* While downsampling is important to break down image and get an idea of 'what' is there, **image segmentation** requires us to do pixel-level labels
* Upsampling can be used to translate this meaning back to the original dimensionality
* Typical techniques include:
	* **Nearest neighbor**, **bilinear**, **bicubic upsampling techniques**
	* **Unpooling**
	* **Transposed convolution** or **deconvolution**

### Nearest Neighbor upsampling
_Simply take the nearest pixel value from the input features_
* Actually works, but can be improved
	![[Pasted image 20240422145738.png|450]]

### Unpooling
_Store indices while max-pooling, use these to reconstruct new values when upsampling_
* Is only used if using [[Week 4 - Convolutional Neural Networks#Max Pooling|max-pooling]]
* When upsampling, put the values to their original positions and put the rest to zero
* Zero-values will later be replaced by the different convolutional layers
* ![[Pasted image 20240422150417.png|450]]
* ![[Pasted image 20240422150818.png|450]]

### Transposed convolution
_Uses kernel functions to upscale 
* Is sometimes also called **deconvolution**, but this term is actually wrong
	* **deconvolution** is actually the inverse of **convolution**, so you get the original features back. In **transposed convolution** you learn a new representation with weights in a higher dimensionality
* Learns parameters of kernel $k$ to enlarge the input
* Stride $s$ and padding $p$ are **not** used for 'sliding' over the input values, but **only** for constructing the new matrix with the values from the kernel
* To use in [[PyTorch basics|PyTorch]]: `nn.ConvTranspose2d`
* You apply the filter once for each input feature. The kernel-weight in the same position as input feature is applied to all the values in the sample.
	* Instead of 'sliding the kernel matrix', you use a kernel-matrix of the same index, based on the current index
	* The kernel slides each value over the input matrix, then the bottom matrices are constructed, based on the stride size
* In the end all the matrices are summed up
* Example with $\text{stride}=1$, $\text{padding}=0$:
	* ![[Pasted image 20240422151432.png]]
* Example with $\text{stride}=2$
	* ![[Pasted image 20240422151959.png]]



## Fetching precise boundary locations

* Earlier high resolution layers have more of the  *where* information, and deeper low resolution layers have more of the *what* information.
* Decoders could benefit from information in the high-resolution layers, as they can help improve finer details
* Two different approaches are [[Week 9 - Object detection#Feature Pyramid Network (FPN)|Feature Pyramid Networks]] and [[#U-Net]]

# Model Architectures
## U-Net
_For each step when encoding the data, store the output and later use it to reconstruct through the decoder_

* Used for **Image Segmentation**
* Originally proposed for medical image segmentation
* Very popular architecture, often used as a baseline
* Simple and powerful
* Performs well on a wide variety of data
* Has many extensions like **UNet++** and **Attention U-Net**
	* **U-Net++** adds convolutions between the encoder-decoder links
* ![[Pasted image 20240422155437.png]]

## DeepLabv3+
![[Pasted image 20240422161129.png|350]]
![[Pasted image 20240422161144.png|450]]



# Instance Segmentation
---
_Classify the different objects individually_
![[Pasted image 20240422161950.png|300]]
* Only label pixels belonging to objects
* Different label for different instances of the same class
## Common solution:
1.  Perform object detection
2.  Generate a Mask for each object in parallel
3. Use **Mask R-CNN**
### Mask R-CNN
* Commonly used, and works well in practice
* Extends [[Week 9 - Object detection#Faster R-CNN|Faster R-CNN]] by predicting mask in parallel to box offset and class
	* A mask is predicted for each class for each **ROI**
* Has many extensions, e.g. **Cascade Mask R-CNN**

* ![[Pasted image 20240422163332.png|450]]

## Main Performance metrics

### Mean IoU
_Performance metric which is defined as the average IoU (Intersection over Union) over all classes_
* Measures the overlap between the bounding boxes of predictions/labels
* The most popular metric, which is pretty much always reported on
* Mainly used for **Semantic Segmentation**
* Steps:
	1. 1. Calculate the **IoU** for each class or instance in the dataset.
	2. Sum all the **IoU** scores.
	3. Divide the sum by the total number of classes or instances, depending on the context.

### Mask mAP
* [[Week 7 - Performance estimation and generalization#Mean average precision (mAP)|mAP]], but here **IoU** (Intersection over Union) is calculated for mask (and not box)
* Mainly used for instance segmentation
### Pixel accuracy
_Fraction of how many of the pixels are correct_
* To mitigate unbalanced classes  it is normal to use **Mean Pixel Accuracy**, which takes the mean of the pixel accuracy of all the classes

### Dice coefficient
_Metric with similar idea as F1-score, but for binary segmentation_
* $\text{Dice}=\dfrac{2\;|A\cap B|}{|A|+|B|}$
* Similar to **IoU** (Intersection over Union)
* Same as **F1-score** for binary segmentation (like foreground vs. background)
* More popular in medical image segmentation domain
* Is used by **UNet++** as loss


## Basic loss functions

* Often modified and tailored for the problem
* Many different application/use-cases

### Semantic segmentation
* Calculate cross entropy for each pixel
* Sum the losses of all the pixels
* Balance for class if required

### Instance Segmentation
* Since it's typically trained jointly with object detection, the loss is the sum of all the three losses: Classification loss, box regression loss, mask loss #toLink 
* The mask loss is calculated just like for semantic segmentation


# Panoptic Segmentation
---
_Combination of semantic and instance segmentation, classify every single pixel but differentiate between each object_

* Combines **Semantic Segmentation** and **Instance Segmentation**
* Each pixel is labeled and different instances of an object class have different labels
* **Terminology:**
	* **Thing**: Object in foreground
	* **Stuff:** Background like grass, mountains, etc.

## Panoptic Quality (PQ)
_Common loss function used for panoptic segmentation_
* Is complicated, and is not part of class curriculum
* #NotImportant

## Different approaches

![[Pasted image 20240422170655.png]]


