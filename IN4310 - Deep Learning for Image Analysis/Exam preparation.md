
* [Recap slides](https://www-int.uio.no/studier/emner/matnat/ifi/IN3310/v24/teaching-materials/recap.pdf)

# Weekly recap
---

## Week 1 - Probability and linear algebra
* Quick general recap of main ideas

## Week 2 - Linear Models
* ERM and gradient descent formulas/update rule
* Linear regression

## Week 3 - Intro Neural Nets
* Logistic sigmoid function
* Cross entropy loss
	* For one-hot labels (in recap slides)

* Hidden layer: $a^{[l]}=g(W^{[l]}a^{[l-1]}+b^{[l]})$

## Week 4 - CNNs
* Output size
	* When whole filter always fits inside input: $(M-k+1)\times (N-k+1)$
	* When filter and input overlaps (with padding): $(M+k-1\times (N+k-1))$
* Padding $p$ changes input shape: $N^{[l]}\times N^{[l]}\rightarrow(N^{[l]}+2p)\times(N^{[l]}+2p)$
* Stride downsampling factor
	* padding $p$, filter $k\times k$, Input size $N\times N$, stride $s$
	* $N^{[l+1]}=\lfloor\frac{N^{[l]}+2p-k}{s}+1\rfloor$
* Standard padding: $p=\frac{k-1}{2}$
* Recursive call for receptive field $R^{[l]}$ with $R^{[0]}=1$
	* $R^{[l]}+(k^{[l]}-1)\displaystyle\prod\limits^{l-1}_{i=1}s^{[i]}$


## Week 5 - Deep Architecture Evolution
* ResNets 
	* residual connections
	* batch normalization after every convolution
	* In top layers: half spatial size of feature maps, and double number of filters
* **Batch Normalization**
	* Normalize activations of a layer to have zero mean and standard deviation one over elements of a mini batch. Then apply a simple affine transformation: ($\gamma,\beta$ both trainable) $y=\gamma\hat{x}+\beta$
	* $BN=\dfrac{x-\mu_{run}}{\sqrt{\sigma_{run}^{2}+\epsilon}}$
	* $y = \text{ReLU}(x + \text{BN}(\text{Conv}(\text{ReLU}(\text{BN}(\text{Conv}(x))))))$
* Fine tuning
	* Low level filters are usually similar, therefore fine tuning is often better (and much cheaper) than pre-training from scratch


## Week 6 - Back propagation and optimization
* Back propagation general formulas
* SGD with mini batch
	* $w\leftarrow \frac{w-\alpha}{B}\sum_{i\in{s_{j}}}\nabla\mathcal{l}_{i}(w)$
* **SGD with momentum**
* **AdaGrad, RMSProp, ADAM**
	* [Blog explaining optimizers](https://www.ruder.io/optimizing-gradient-descent/)


## Week 7 - Performance estimation
* k-fold cross validation
* **Representability**
* External datasets
* Controlling networks capacity
	* Reduce number of trainable parameters
		* Stack conv layers with smaller kernels
		* Depthwise separable convolutions
		* Reduce width (channels) and depth (num layers)
		* Should be scaled according to input size (image resolution)
	* Dropout
	* Weight decay
* Facilitating generalisation
	* Color augmentation
	* Stain normalization
	* [[Week 7 - Performance estimation and generalization#Cycle-GAN|Cycle-GAN]]
		* Get a training and target image. Make training image gradually more like target image during training
* Normalization
	* Dataset-based can facilitate faster training convergence (all images transformed using same function and parameters)
	* Image-specific normalization can make images more similar
* Confusion matrix, precision and recall (pr-curve)
* **Average Precision**
* **Sensitivity and Specificity**
	* Sensitivity=recall
	* Specificity=true negative rate (calculated on TN instead of precisions TP)
* **ROC curves**
	* Same as precision-recall curve, but with sensitivity and specificity
	* **AUC/AUROC** is the area under the ROC curve
* Balanced accuracy
* "Key learning goals"
	* ![[Pasted image 20240527193236.png|200]]

## Week 8 - Data Augmentation
* Distributional shifts, out of distribution samples and outliers (different distributions in datasets)
	* Resolution, scale, perspective, pose, lighting, colors, label distribution
* Methods for generalization and domain adaptation
	* Down-sampling with pooling layers
* Image augmentation
	* geometric (size, shape, position, orientation,...)
	* photometric (brightness, contrast, color, noise, solarization,...)
	* other (blur, edge filters)
* Methods for fixed NNs on varying inputs
* Weight init strats
	* Identity: $W_{\theta}x=Ix=x$
	* Orthogonal: Sample orthogonal matrix
	* Random: Sample the parameters
	* Pre-trained: Use weights from another neural network
* Contrastive learning
* More stuff...

## Week 9 - Object Detection
* One-stage detectors
	* Directly predict bounding boxes
	* On final feature map slide a window and predict an object class and a bounding box for each anchor
	*  **Single Shot multibox Detector (SSD)**
* Two-stage detectors
	* First find candidates, then process each candidate individually
	* **Feature Pyramid Networks (FPN)**
		* Also used as backbone in one-stage detectors like EfficientDet
		* Since deeper layers usually gives semantically stronger features, send output of earlier layers into later layers
		* ![[Pasted image 20240527200438.png|200]]
* R-CNN
	* First run selective image search on image for candidates, then run CNN for each candidate separately
* Fast R-CNN
	* First run selective image search on image for candidates, then run one CNN over the whole image. Then predict bounding boxes and labels on the output feature map of CNN using ROI Pooling
* Faster R-CNN
	* Same as faster but uses two CNNs for candidates
	* CNN runs on GPU not CPU
	* First pretrained CNN to extract features, then a CNN (Region Proposal Network) to make actual proposals based on extracted features
* Anchors
* **Non-maximum suppression**
* Focal loss
* IoU

## Week 10 - Image Segmentation
* The three problems:
	1. How to capture global context?
		* Downsample feature maps
			* Increases receptive field
		* Dilated/atrous convolution
			* Increases receptive field to larger part of image
	1. How to upsample features?
		* Nearest neighbor upsampling
		* Unpooling
		* Transposed convolution
	2. How to fetch precise boundary locations
		* Feature Pyramid Network, UNet
		* Dilated/atrous convolution
* Semantic Segmentation
	* Detect object classes and background classes
* Instance Segmentation
	* Detect specific objects within object classes
	* **Mask R-CNN**
		* First R-CNN for class segmentation
		* ...
* Panoptic Segmentation
	* Combination of semantic and instance segmentation
* Mean IoU
	* Average IoU over all classes
	* Mainly for semantic segmentation
* Mask mAP
	* Similar to [[Week 7 - Performance estimation and generalization#Mean average precision (mAP)|mAP]], but IoU is calculated for mask
	* Mainly for instance segmentation
* Performance metrics
	* Pixel accuracy
	* Mean pixel accuracy
	* Dice coefficient
		* Similar to IoU, same as F1 score for binary segmentation (foreground vs background)
		* $\dfrac{2|A\cap B|}{|A|+|B|}$


## Week 11 - Adversarial attacks
* White box attacks
	* We have full access to model/weights
* Black box attacks
	* We to not have access to params, just outputs
	* Surrogate attacks
		* Train a surrogate model and attack the surrogate with a white box method. Assume the attack on the surrogate model model generalizes to target model
	* Boundary attacks
		* Starts with a random image and iteratively refines the adversarial example by moving it closer to the decision boundary
		* Without gradient, use a hill-climbing approach
* Adversarial image
	* Image which has been slightly modified with the goal of tricking classifier
* Targeted attacks
	* Trick network to classify a sample $x$ into a fixed class which is wrong
* Untargeted attack
	* Trick network to classify an adversarial image, without a target class
* Projected gradient methods
	* Use gradient ascent iteratively to update perturbation's to increase the loss of the input image
* Defensive methods
	* Adversarial training
		* Find universal adversarial perturbation $\delta$ with Projected Gradient Descent, perform standard forward and backward pass of you network using $\delta$
		* Is expensive and decreases predictive power
	* Denoising in preprocessing
	* Quantization
		* Smaller changes removed
	* Ensemble defense
		* 
* Well-posedness (opposite is ill-posed)
	* Problems where a solution exists, is unique and changes continuously with the input
* Ill-conditioning
	* Small changes in input can lead to big changes in output

## Week 12 - RNNs
* **BackPropagation Through Time** (BPTT)
	1. Unroll the TNN in the time dimension
	2. Apply backpropagation on the unrolled RNN by treating it as a regular feed-forward network
* **Truncated BPTT**
	* Stop at some point during the sequence to update the weights
	* Allows us to not keep the whole sequence with all the hidden states in memory before updating weights
* Exploding/vanishing gradients
	* Gradients grow either too big or too small for longer sequences
* LSTM
	* Input gate
		* How much of new memory is addd to the cell state (long term memory) (sigmoid and tanh hadamand product of input)
	* Forget gate
		* How much of cell state to forget ()
	* Output gate
		* How much of updated memory to output (sigmoid from input, tan cell state, hadamand product)
* GRU
	* Simpler LSTM
	* Combines Input gate and forget gate into a single update gate
	* Merges the cell state and the hidden state
* Bidirectional RNNs
	* Looks at 'future' tokens
	* Traverses input in both directions, once forwards, then backwards

## Week 13 - Vision Transformers
* Attention
	* Alignment function takes query, key and value vectors to compute attention
		* Additive attention
		* General attention
		* Dot-product attention
		* Scaled dot-product attention
			* Used in transformers
	* Helps with vanishing gradient problem, and no sequential bottleneck
	* Allows some interpretability
		* By looking at attention weights, we can determine what the decoder focused on
	* By design attention is **permutation equivariant**, in order to fix this we use **positional encodings**
		* Multiple variants: absolute/fixed, relative, hybrid, learned,...
		* Vectors with same dimension as the input vectors
		* Usually added to the input vectors
* Vision transformers
	* Convert pixels to sequence of colors and send as input to standard transformer
	* Since $N\times N$ image has $N^{2}$ pixels, if you send whole image it is too expensive, as it will take $O(N^{4})$. Instead we do it on patches
	* Steps:
		1. (Optional) add classification token `[CLS]`
		2. Convert image to linear D-dimensional vector
		3. Add learned positional embedding
		4. Send through transformer model
* ViT vs CNNs
	* In CNNs the resolution decreases and number of channels increases as we go deeper. In ViT these stay the same
* w
* DETR
	* Object detection pipeline: directly output a set of boxes from a transformer
	* Anchor free approach, i.e., no pre-defined anchors are used
	* No [[Week 9 - Object detection#Non-max suppression|NMS]] is used, it is learned by transformer automatically
	* Match predicted boxes to ground truth boxes with bipartite matching
	* Steps:
		1. CNN is used to extract features from the input ($1\times1$ conv layer is used to reduce the number of channels)
		2. Fixed positional encodings are added to every encoder blocks input
		3. Standard transformer encoder is used to process the flattened image features
		4. Encoder output is sent to transformer decoder, with randomly initialized query vectors (object queries)
		5. The decoder is used to generate the outputs, one vector per object query
		6. Vectors from decoder gets sent through each their own FFN, and returns either a class box or "no object"






