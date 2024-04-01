
# Model compression
---

* The trend is an exponential growth in the scale of the models, therefore it is highly beneficial to make the models smaller to require less resources
* ![[Pasted image 20240329222934.png|300]]


## Impacts of computational race
* Scaling the number of parameters in **LM**s facilitates new state-of-the-art results, however...
* It significantly increases the carbon footprint
* Facilitates the problem of unequal access to computational resources
* Promotes difficulties using such models in academia and industry

## Techniques to improve efficiency

* ![[Pasted image 20240329230751.png|400]]


## Pruning
_Identify and remove redundant parameters_

* Pruning during pre-training reduces the costs but increases the risk of over-pruning
* Additional costs can relate to tuning the hyper-parameters as the number of preserved weights

![[Pasted image 20240329231344.png|450]]
### Unstructured pruning 
_Zeroing out parameters below a threshold_
* May better preserve the model performance

### Structured pruning
_Removing model components_
* May better improve inference speed
* Remove components like for example
	* Attention heads
	* Hidden layers

## Knowledge Distillation
_Knowledge distillation aims to pre-train a smaller LM (student) that mimics the behavior of the original LM (a teacher)_

* The student has fewer weights and achieves a performance similar to that of the teacher
* **DistilBERT** is an example of such a model
	* Initialized from [[Week 6 - Decoder and Encoder Based Language Models#BERT|BERT]] by taking one out of two layers
	* Pretrained using a linear combination of the distillation and masked language modeling losses
	* Compared to [[Week 6 - Decoder and Encoder Based Language Models#BERT|BERT]] it has 40% less parameters, is 60% faster and retains 97% of the language understanding performance on **GLUE**
* ![[Pasted image 20240329232427.png|350]]


# Parameter-efficient fine-tuning
---






