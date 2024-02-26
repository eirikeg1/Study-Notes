_There are three kinds of attention used in Transformers_

* In [[Week 10 - Dialogue Models#Encoder-decoder models|encoder-decoder models]] we use hidden state from the encoders and do some operation with the state in the decoder
* Encoder Self-Attention: each position in the encoder can attend to previous positions
* Decoder Self-Attention: The same as Encoder Self-Attention, but with **masking**: Each position can attend to all previous positions up to that point (autoregressive via masking)

![[Pasted image 20240226002215 1.png|300]]
# Self-Attention (Intra-Attention)
---

* Is the Multi-Head Attention module in the Transformer Encoder 
* $Attention(Q,K,V) = softmax(\frac{QK^T}{\sqrt{d_{k}}})V$

## Steps

![[Pasted image 20240226002406 1.png|300]]

1. From each input, create the **Query**, **Key** and the **Value** vectors	
2. Calculate a score for each of the words in the input sequence against other tokens in the sequence:
	* $Q_{q}\cdot K_{1}= 31$
	* $Q_{1}\cdot K_{2}=21$
3. Divide each score by the root of the dimension of the key vector ($\sqrt{d_k})$)
	* $x_{q}=(Q_{1}\cdot \frac{K_{1}}{\sqrt(d_{k}} = \frac{31}{\sqrt{3}}$
4. Softmax that score
	* $\alpha_{1}=Softmax(x)$
5. Multiply the softmaxed score with the Value vector
	* $Attention_1=\Sigma_{i=1}^{n}{Z_i}$

### In practice
* In practice, we use matrices, not vectors
* $X$ has `row_count` number of words, each represented with a `col_count` dimensional vector
* Problem if $\sqrt{d_{k}}$ becomes to large the gradients becomes very small, which is bad for learning
	* We will _push_ the softmax, creating small gradients
	* Solution: Scale down the dot pruducts by $\frac{1}{\sqrt{d_{k}}}$
* The two most used attention functions are **Additive-Attention** and **Dot-Product Attention**, while both are similar in theoretical complexity, dot product attention is much faster and more space-efficient in practice, since it can be implemented using highly optimized matrix multiplication code
* ![[Pasted image 20240226003647 1.png|300]]
* ![[Pasted image 20240226003737 1.png|300]]

### Multi-Head Attention
* Have multiple sets of $Q$, $K$ and $V$ matrices, to create differently learned linear projections
* In original paper, $h=8, d_{k}=\frac{d_\text{model}}{h}=64$
* Calculate $h$ different attention matrices, concatenate them and linearly project them
* Just as computationally costly, since we concat 64-dim matrices 8 times, compared to projecting a 512-dim matrix once
* Allows model to jointly attend to information from different representations:
	* ![[Pasted image 20240226005300 1.png|300]]
	* 
