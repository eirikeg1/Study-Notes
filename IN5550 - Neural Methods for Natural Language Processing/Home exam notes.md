

* Modify number of Bias terms? [[Mehta et al - OpenELM - An Efficient Language Model Family with Open Training andInference Framework|Mehta et al 2019]]
* Different attention? [[Mehta et al - OpenELM - An Efficient Language Model Family with Open Training andInference Framework|GQA?]]
	* Decreases the number of trainable parameters
	* Not for encoder [GQA paper](https://arxiv.org/pdf/2305.13245)
* **Linformer**
	* Good for long range efficient attention
* Knowledge distillation?
	* Consider using a larger model as a teacher (if allowed)
* **Pruning during training**
	* Is this allowed for assignment? Can the model exceed the max parameter count in the initial layers?
* Parameter sharing
	* Share parameters in some of the Feed Forward Layers, especially in earlier Transformer Blocks
	* [Lessons on Parameter Sharing across Layers in Transformers](https://arxiv.org/pdf/2104.06022)
* [Universal Transformers](https://arxiv.org/pdf/1807.03819)
	* State of the art for LAMBADA (2019)
	* Recurrence over transformer blocks
	* Good for parameter reduction
	* Does recurrence for more ambiguous symbols, can be good for small vocabulary




