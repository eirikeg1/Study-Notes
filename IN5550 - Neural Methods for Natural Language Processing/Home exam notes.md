

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

# Training
---
## Pipeline
### Step 1
2\*3\*3=18
* Test Deep-Wide
* Sharing: 6, 8, 12
* Seq, cycle, cycle_rev

### Step 2
4
* Test best assignment strategies and sharing size on Deep and Wide models

### Step 3 (optional)
2
* If wide or deep outperforms deep-wide, test alternative deep-wide configurations

### Step 3
6
* 25.000 steps

### Step 4
2
* 5 hours

### Step 5 (optional)
6

## Configs
### Deep
* Num hidden layer

### Wide
* Hidden Size
* Intermediate size

### Deep-Wide FFN
* Num hidden layers
* Hidden Size
* Intermediate size


# Results
---

## Training run 1
### BLiMP

| Config              | Dec 10k   | Enc 10k   | Dec 25k   | Enc 25k   |
| ------------------- | --------- | --------- | --------- | --------- |
| Baseline            | **71.02** | 48.44     | **71.09** | 47.58     |
| deep_seq            | 70.00     | 49.73     | -         | -         |
| deep_cycle          | 67.56     | 48.03     | -         | -         |
| deep_cycle_rev      | 69.31     | 50.38     | 70.6      | 50.06     |
| very_deep_seq       | 69.67     | 48.49     | -         | -         |
| very_deep_cycle     | 65.60     | 49.13     | -         | -         |
| very_deep_cycle_rev | 69.84     | 51.04     | 70.15     | **51.43** |
| wide_seq            | 70.05     | 43.98     | -         | -         |
| wide_cycle          | 70.05     | 44.66     | -         | -         |
| wide_cycle_rev      | 70.05     | 43.98     | 69.24     | 45.35     |
| very_wide_seq       | 65.32     | **52.78** | -         | -         |
| very_wide_cycle     | 67.58     | **52.78** | -         | -         |
| very_wide_cycle_rev | 66.89     | **52.78** | 70.06     | 50.24     |
| wide_deep_seq       | 68.40     | 51.90     | -         | -         |
| wide_deep_cycle     | 68.71     | 51.90     | -         | -         |
| wide_deep_cycle_rev | 68.40     | 51.71     | 70.72     | 49.97     |

### Lambada
| Config              | Dec 10k      | Enc 10k          | Dec 25k       | Enc 25k         |
| ------------------- | ------------ | ---------------- | ------------- | --------------- |
| Baseline            | **8.3 (22)** | 0.0 (1374)       | 8.93          | 1.998 (823)     |
| deep_seq            | 7.1 (23)     | 0.078 (1094)     | -             | -               |
| deep_cycle          | 7.4 (23)     | 0.0 (1428)       | -             | -               |
| deep_cycle_rev      | 7.22 (23)    | 0.0 (1418)       | 7.65 (22)     | **2.562 (551)** |
| very_deep_seq       | 6.8 (24)     | 0.076 (1712)     | -             | -               |
| very_deep_cycle     | 5.96 (27)    | 0.058 (2043)     | -             | -               |
| very_deep_cycle_rev | 6.66 (24)    | 0.19 (1384)      | 7.14 (22)     | 1.087 (1069)    |
| wide_seq            | 6.79 (25)    | **0.194 (1623)** | -             | -               |
| wide_cycle          | 6.8          | 0.0 (1923)       | 4.09 (28)     | 0.097 (1248)    |
| wide_cycle_rev      | 6.79 (25)    | 0.194 (1709)     | **9.84 (19)** | 0.78 (973)      |
| very_wide_seq       | 0.37 (54)    | 0.0 (2175)       | -             | -               |
| very_wide_cycle     | 0.97 (40)    | 0.0 (2175)       | -             | -               |
| very_wide_cycle_rev | 0.89 (38)    | 0.0 (2175)       | 8.95 (20)     | 0.0 (3544)      |
| wide_deep_seq       | 6.58 (24)    | 0.19 (1232)      | -             | -               |
| wide_deep_cycle     | 6.23 (25)    | 0.019 (1232)     | -             | -               |
| wide_deep_cycle_rev | 6.58 (24)    | 0.175 (1244)     | 9.33 (20)     | 1.144 (983)     |




# Plan Paper
---

# Present Results
## BLiMP
### Encoder
* Rayyan writes about his findings on the **encoder**
* Slight improvement generally, but not much
* Marginal differences overall, low values across the board

### Decoder
* On the decoder we did not get any improvements
* Increasing number of steps makes the difference between the parameter-sharing and baseline lower, **perhaps** this scales better with more training?
* Adding parameter sharing did not seem to affect the result a lot.

## LAMBADA
### Encoder
* Overall bad results across the board
* Both baseline and parameter sharing models improve with number of steps, however they seem to be similar

### Decoder
* Decoder **baseline** around 7.9-8.4. With the best being 8.95 at 10.000 steps
* Shared_6_cycle_reverse at 9.06 at 10.000 steps
* Generally quite similar results at 10.000 steps
* Decoder seems to scale better with parameter sharing, as most runs at 25.000 steps are generally better than in 10.000. The best overall model was a wide parameter sharing model with 9.84. Best baseline was 8.93

## Conclusion/summary
* Overall our encoders did pretty bad on these metrics. However it seemed that they  got a slight improvement on BLiMP, but still pretty bad scores.
* Decoder did seem to improve at LAMBADA, but not on BLiMP. 




# Other stuff
---
\begin{equation}
\small
  \label{eq:example}
  MultiHead(Q,K,V) &= Concat(head_{1}, \cdots, head_{h}) W^{O}
\end{equation}

\begin{align*}
\small
\text{ MultiHead}(Q,K,V) &= \text{Concat}(head_1, \ldots, head_h)W^O \\
\end{align*}

\text{\small where each $head_i$ is computed via,}

\begin{align*}
\small
\text{Attention}(QW_i^Q,KW_i^K,VW_i^V) \\

\end{align*}

\text{\small and,}
\begin{align*}
\small
\text{Attention}(Q,K,V)=
softmax(\frac{QK^T}{\sqrt{d_k}})V \\

\end{align*}

