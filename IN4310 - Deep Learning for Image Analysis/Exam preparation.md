
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

