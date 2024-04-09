
# What we need
---

* Parallel **data** for training
* [[Vaswani et al - The Annotated Transformer#Encoder-Decoder|Encoder decoder transformer]]
* Evaluate the trained model


# Data
---
## Parallel corpus (bitext)
_Set of sentence pairs with same meaning, in different languages_

* Typically one is original text, other has been translated by a human
* Typical data sources:
	* International political organizations
	* Movie subtitles
	* The bible or other aligned-literature (Bible is sections into different verses)
	* Multilingual websites (Web crawl)

### Noise in parallel corpora
_There can be multiple challenges in parallel corpora_
* Not translated directly
* Very similar languages (model can be confused what it is translating from)
* 
![[Pasted image 20240408123521.png|350]]
* Table below shows how much noise (errors) was found in different corpora
	* ![[Pasted image 20240408123714.png|350]]

### OPUS
_One of the most popular parallel corpora_
* [OPUS website](https://opus.nlpl.eu/)
* It is useful to filter/clean the dataset before using them
* By adding noisy data to the data, the score goes down substantially
	* ![[Pasted image 20240408123910.png|350]]
* [OpusFilter](https://github.com/Helsinki-NLP/OpusFilter) is a parallel corpus filtering toolkit
	* Absolute length and length differences
		* Similarity in terms of punctuation, numbers, ...
		* Language and script identification
		* Language model scoring
		* Word alignment success rate
		* Sentence alignment success rate
		* 

## Sentence alignment
_Often not possible to translate all sentences one-to-one directly between languages_

### The Gale & Church algorithm
* Completely language independent
* Sentences cannot be split, but they can be merged
* Difference between number of characters is a good indicator whether two strings are translations of each other
* Following mappings exist (with decreasing probabilities):
	* 1-1
	* 1-2
	* 1-3
	* ...
* ![[Pasted image 20240408122914.png|350]]

## Data augmentation
_Create synthetic parallel data_

### Simple approach
_Works surprisingly well_
1. Find monolingual text in the target language
2. Pair it with some automatically generated text in the source language

### Back-translation
* Create an **auxiliary MT system** in the opposite direction
* Train the auxiliary model to get a dataset in the opposite direction
* ![[Pasted image 20240408124738.png|400]]


# Data preprocessing and hyperparameters
---
## Hyper-parameter tuning

* Most efficient MT models combine a deep encoder with a shallow decoder

## Tokenization approaches
* [[Week 12 - Machine Translation#Byte Pair Encoding|Byte pair encoding]]
* [[Week 12 - Machine Translation#Sentence piece|SentencePiece]] is most popular
* Subword regularization/sampling
	* Choose different subword segmentation when training model
	* Makes model more robust to different segmentations
	* Helps against typos
* **Character-based** or **byte-based** models
	* Very long token sequences, slow to train
	* Can generalize to new scripts
* **OCR**/pixel-based approaches
	* Take a screenshot of input text, let vision model generate output


# Evaluation metrics
---

## String based
_Compare the string similarity_
* [[Week 12 - Machine Translation#The BLEU score|BLEU score]]
	* Word n-gram overlap
* [[Week 12 - Machine Translation#chrF character-level score|chrF score]]
	* Character-level comparison
	* Gives points if part of word is correct

## Semantic (embedding based)
* BERTScore

## Trained metrics
* [[Week 12 - Machine Translation#Trained Metrics (e.g COMET)|COMET]]
	* Produce sentence embeddings for source $s$, hypothesis $h$ and reference $r$
	* 


# LLMs for machine translation
---

* Even though they are not explicitly trained on parallel data, there are a lot of 'translation signals' even in monolingual data (**incidental bilingualism**)
* 

