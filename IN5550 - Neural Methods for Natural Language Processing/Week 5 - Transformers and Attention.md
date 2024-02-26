
# Transformer Architecture
---

* [[Week 8 - Transformer Models|Notes from IN4080]]
* BER**T**, RoBER**T**a, BAR**T**
* Text-to-Text transfer Transformer
* Neural model based solely on attention
* Performs better than the older models (image showing the [[Week 12 - Machine Translation#The BLEU score|BLEU score]]):
	* ![[Pasted image 20240226010814 1.png|300]]

![[Pasted image 20240226000804.png|400]]

## Self-Attention
---

* In classic [[Week 10 - Dialogue Models#Encoder-decoder models|encoder-decoder model]], attention is calculated between the decoder and all the hidden states from the encoder

![[Pasted image 20240226000901.png|400]]

### Intra-level
_Attention between different things within the same sequence_
* In many cases the meaning of the word needs the context
* For example the word **The**, usually would need more attention to the following word/s
* ![[Pasted image 20240225235845.png|400]]
* ![[Pasted image 20240225235932.png|450]]

## Encoder and Decoder
---

### Encoder
* Uses Self-attention to transform input to output representation of weights
* A [[Week 2 - Multi-layered Networks and Deep Learning#Feed-forward neural networks|Feed-Forward Neural Network]]
* 
* ![[Pasted image 20240226001129.png|200]]
  

### Decoder

* Uses **Masked Self-Attention** to avoid looking into the future ([[Week 8 - Transformer Models#Masked language modeling|Masked language modeling]])
* Autoregressive property of transducers

### Encoder-Decoder attention

* Calculate the attention between decoder and encoder hidden states (inter-level)
* [[Week 8 - Transformer Models#Encoder-decoder models with cross-attention|Encoder-decoder with cross attention]]

## Positional encoding
---

* Because all calculations are done in parallel, the model has no sense of word ordering
* Running numbers (index of word) are not very efficient as values would get large and lengths not seen during training could show up during evaluation
* Add running number from $[0,1]$ is also not great, as it is not given how many words there are in a specific range. It is not consistent across sequences
* We need a unique encoding for each timestep

### Sine and cosine wave matrices
_Used to encode the word order_

* Add a vector of sine and cosine matrices to the embedding
* ![[Pasted image 20240226010058 1.png|300]]
* ![[Pasted image 20240226010142 1.png|300]]
* $i= \text{dimension index}, d_{\text{model}}=\text{embedding size}, pos=\text{position of the word we are calculating}$
* If the size of embeddings is 4, so $d_{model}=4$, then $d_{P}=4$, which gives us four waves with different frequencies:
  ![[Pasted image 20240226010445 1.png|300]]
* Then, the positional encoding for time step _pos_ is the column vector at $x=pos$ in the figure above
