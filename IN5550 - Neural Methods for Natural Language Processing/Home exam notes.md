


* Modify number of Bias terms? [[Mehta et al - OpenELM - An Efficient Language Model Family with Open Training andInference Framework|Mehta et al 2019]]
* Different attention? [[Mehta et al - OpenELM - An Efficient Language Model Family with Open Training andInference Framework|GQA?]]
	* Decreases the number of trainable parameters
	* Not for encoder [GQA paper](https://arxiv.org/pdf/2305.13245)
* **Linformer**
	* Good for long range efficient attention
* **Pruning during training**
	* Is this allowed for assignment? Can the model exceed the max parameter count in the initial layers?
* Parameter sharing
	* Share parameters in some of the Feed Forward Layers, especially in earlier Transformer Blocks
	* [Lessons on Parameter Sharing across Layers in Transformers](https://arxiv.org/pdf/2104.06022)
	* 