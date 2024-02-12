

# Traditional methods
---
**This topic is coved in IN4080**
* [[Week 5 - Sequence labeling 2#Bigram Hidden Markov Models]]
* [[Week 4 - Sequence Labeling]]
* [[Week 5 - Sequence labeling 2]]


## Old way

![[Pasted image 20240212102149.png|500]]


# Deep learning and language models
---

* Concatenate learned embeddings of the previous k words
* Feed this concatenation into a [[Week 7 - Neural networks#Feed forward neural networks|feed forward neural network]] with hidden layers and non-linearity
* Output probability distribution over possible next words across the vocabulary $V$, using softmax and the second embedding matrix

![[Pasted image 20240212105146.png|400]]


## Modern state of the art

* Based on either RNN #toLink or [[Week 8 - Transformer Models|Transformer models]]
