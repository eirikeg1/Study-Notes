


## Differences in distributions

* Different resolutions, scales, perspectives, poses
* Lighting, colors
* Different label distributions
![[Pasted image 20240311102624.png|350]]


## Terminology 

* **Generalization**
* **Domain adaptation**
* **Out of distribution**
	* Samples significantly different from what model is trained on
* **Outliers**
	* Samples from tails of training or target distributions
* **Distribution shift**
	* Samples with different statistical properties from the data our model was trained on


## Preparation techniques

* **MinMax**
* **MaxAbs**
* **Standardization**


# Artificially extending our dataset
---

* Often done on the fly when fetching the data (from dataloader), so dataset is not changed

## Validation set
* Not common, except for very small things in some cases

# Transformation techniques
---
## Geometric image transformation
* Changes to geometric properties
* Sizes, shape, position, orientation, etc
* Affine is a generalisation of rotating and flips, with shifting, scaling and shearing
* Flips can be bad for flags, e.g. Ireland and Ivory coast
	* ![[Pasted image 20240311105042.png|250]]
* Can be done easily in [[PyTorch basics|PyTorch]]
	* ![[Pasted image 20240311103547.png|250]]
	* ![[Pasted image 20240311103608.png|250]]
	* ![[Pasted image 20240311103903.png|300]]

## Photometric transformations
* Photoreceptive changes
* Brightness, contrast color, noise 
* Standard method
	* Random perturbation of either channel in HSV/HSL space
	* Note: Hue channels are angular
* **PyTorch**:
	*  ![[Pasted image 20240311104027.png|300]]

### HSV
_Color manipulation_
![[Pasted image 20240311104139.png|300]]


### Solarization
_Image where colors above a certain threshold is inverted_
* Implemented using **PIL** library, or `torchvision.transforms.RandSolarize`:
	* ![[Pasted image 20240311104300.png|300]]

![[Pasted image 20240311104229.png|300]]
## Other
* Blur, edge filters

### Blurring
_Applying a low-pass-filter, removing high frequency components out of the image_

* Usual to use a Gaussian kernel
* Often done on CPU while GPU is doing calculations, so it is ready when GPU wants to use it
* Using **PIL**:
	* ![[Pasted image 20240311104451.png|300]]

### RandAugment
_Random combination of 14 different photometric and geometric transforms, with little inference_

### Mixup
_Pairs all images in batch, blends with random convex combination_
* Blends labels and images
* ![[Pasted image 20240311104741.png|300]]

### Cutmix
_Pairs all images in batch, picks random bounding box in the image, and copies slice from one image to another_
* Blends labels and images
* ![[Pasted image 20240311104754.png|300]]


### Label Smoothing
_Instead of optimizing p(y|x) directly, assume the label is correct with a probability, and distribute the rest of the probabilities to other images_
* Regularizer


# Other domains
---
## Video and audio

* Lots of existing work of filters and transformations
* Can be hard to augment in other domains

### Additive noise
* Has to be similar to real world noise, not necessarily gaussian

### Sampling from generative models


## Compared to NLP

* Language is categorical, images are continuous
* Ordering in language is grammar dependent, less clear cut order
* Uses [[Week 8 - Transformer Models#Masked language modeling|Masking]]
* Synonyms can be replaced by **KNN** on [[Week 3 - Count-based distributional semantic models#Use of embeddings|word embeddings]]
* 


# Other techniques
---

## Image size
* Simple approach, scale images to match network size
* Convolutions can work on different image sizes
	* Down-sampling with global pooling
		* ![[Pasted image 20240311111639.png|250]]
* **Vision transformers** (**ViT**) can support different sizes

### Pooling operations in CNNs

 * Can help by supporting images of different sizes
 * Global pooling can be used, often before the last fully connected layers
 * ![[Pasted image 20240311111733.png|300]]


## Weight initialization

### Identity initialization
_Initialization by identity matrix_
* Forces model to learn correlations between features
* Unit gradients $\rightarrow$ optimal gradient propagation
* Better for later layers
* Ignores layers with fewer output dimensions
* Can take longer to train

### Orthogonal initialization

* Orthogonal matrix definition: $A^{T}A=AA^{T}=I$
* ![[Pasted image 20240311112638.png|200]]
* Similar properties to identity, optimal gradient prop, no correlation or bias
* Initially invariant to rotation and scaling, can lead to better generalization
* Limited applicable to smaller networks
* Only square matrices
* Tricky to initialize for convolutions

### Random initialization
_Most common method in practice

* Commonly use a normal/gaussian distribution or uniform distribution with zero mean for weight initialization
* Computationally efficient
* Uniform and normal distribution have no assumptions (non-informative choice)
#### Asymptotic orthogonality
* If we take the grammian ($A^{T}$?), we get something which looks like an identity matrix
* Can give some nice properties from other initialization techniques

### Weight normalization

* ![[Pasted image 20240311113353.png|300]]

### Standardization
* Instead of normalizing to unit norm, standardize to zero-mean unit variance
* Batch norm not useful sometimes #Maybe 
* ![[Pasted image 20240311113621.png|300]]
* ![[Pasted image 20240311113531.png|300]]

### Other common initializations

* **Sigmoidal**
	* Derived by Xavier Glorot
* **Rectified**
	* Derived by Kaiming He


## Transfer Learning
_Take weights from other network which was trained on similar task, then initialize with that_

* Leverage what has been learned before
* ![[Pasted image 20240311114124.png|250]]


## Student-Teacher Learning
_Train a smaller student model from a large/complex teacher model_

* Train student model by using the softmax output of the teacher model as soft labels
* **Cross-entopy loss** using teacher output as ground truth labels
	* Prioritizes learning easier samples (easy samples when class probabilities are all close to $\frac{1}{C}$)

## Contrastive Learning
_Pre-train dataset without labels, use augmentations to create two different 'views' of the same image_

* Train network to recognize augmented instances of the same image
* Augmentations of same image should have high similarity scores
* ![[Pasted image 20240311120006.png|200]]

### SimCLR version
* Sample mini-batch
* Create two views of each image by applying random selection of simple augmentations
* 
* Contrastive loss:
	* ![[Pasted image 20240311120117.png|300]]
* Requires very large batch sizes



