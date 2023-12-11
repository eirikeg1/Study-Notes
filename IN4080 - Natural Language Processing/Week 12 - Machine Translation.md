
# History

* Rule based between 1950-1980
	* Machine translation was paused around 1966 as it was reported as expensive and inaccurate
* Example based machine translation from 1980-1990
* Statistical Machine Translation 1990-2015
* Neural Machine Translation 2015-Today

# Sequence to sequence models
* MT is a seq-to-seq problem
* Can be split into MT (english to Japanese)
	* Modernisation/normalization (old english to modern)
	* Lemmatization (inflected word form to base form)
	* Style transform (colloquial english to formal english)

# Multilingual translation models

* Transformer models can often learn several languages between each other by appending language labels in dataset
	* e.g $<FROM\_ES>,<TO\_FR>$ 
	* Source label can also be removed, often it does help but can work without
* **Zero shot translation**
	* Can learn to translate from one language to another, even though that specific pair was never in training data

# Different Models
---

# Rule-based MT

1. Build dictionaries
2. Write transformation rules
3. Refine, refine, refine

* Commercial applications
	* 1976: Weather forcast translation French-English
	* 1968: Systran

# Statistical MT

* 1990: Also known as **IBM models**
* Learn everything from a parallel corpus
	* Two corpus with same sentences in the same order
	* Learn which words can be translated to other words, and what words changes order in what contexts
* mid-2000s:
	* A lesson EBMT: Translating each word separately is harder than it needs to be
	* Keep frequent word sequences together and translate them as a whole
* Late 2000s:
	* Commercial viability (Google Translate)


# Neural MT

* Late 2000s: Successful use of neural models for computer vision
* 2012, 2013: first neural models for MT proposed
* Since 2016: NMT is the new state of the art


# Data-driven MT


## Task
* We have a source sentence which should be translated to a target language
* Meaning has to be the same in both languages

## Training data
* To train we need a parallel corpus or bitext (set of sentence pairs from input language to target language)
* Rule of thumb: at least 1 million sentence pairs
* Can be found from 
	* movie subtitles
	* International political organisations and national organisations of multilingual countries
	* Translated literature or websites
	* OPUS corpus collection (often best to avoid copyright problems)

# NMT model architecture

* Most popular architecture is the **Transformer**

## Encoder-decoder with attention
* Encode source sentence
* Then decode the target sentence by attending the most relevant source tokens

# Open vocabulary translation
---

# Representing words

* Words are translated to a vector of numbers
* Input is usually one-hot encoding of source words
* Because vectors are usually huge, this becomes an expensive method

* Training corpora typically contain millions of word types
* Morphological processes (inflection, derivation, compounding) allow formation and understanding of unseen words
* No training corpus contains all existing names, numbers etc.

### Large vocabularies
* Increase the memory requirements
* Decrease training and decoding speed
* Still not large enough

### Unkown word tokens
* Limit the vocabulary vectors to the $n$ most frequent words
* Add one reserved cell for all rare and unknown words: $<UNK>$

### Bank of models
* Replace rare words with $<UNK>$ at training time
* When system produces UNK translate with a back off method, fex dict
* Back off could potentially be cross attention, can work well
* Limitations
	* Compounds hard to model 1 to many relationships
	* Morphology: hard to predict inflection with back off dictionary
	* Names: if alphabets differ we need transliteration
	* It is quite hard to determine the source language of a single word

### Character-level translation #toExpand 
* Only use $<UNK>$ For used unknown characters
	* Limitations:
		* Still many UNKS for languages with large character sets (chinese)
		* Increasing sequence length slows training/characterising time

### Hierarchical models
* Hybrid between the two above
* Encode each word as a sequence of characters
* When the model produces $<UNK>$ in the output, back off to a character level decoder


### Subword Units
* Split words into pieces of variable length
	* Usually longer than single characters, but shorter than enitre words
	* Frequent words should often be more split up than rare words
* Ideally in morphologically sensible way
	* Suh that anu unseen words can de decomposed into subwords
* Without using any external tools #lecture 

#### Subword segmentation schemes
* Byte pair encoding (**BPE**) (original)
* Morfessor
* SentencePiece unigram model (since 2019)

#### Byte Pair Encoding
1. Start with a vocabulary of a single character and a dictionary over word frequencies
2. Iterate over dictionary and record number of occurrences of everything in vocabulary concatenated with every single word into an ngram
3. Merge most frequent ngrams pairs into the vocabulary
4. Stop after k merging steps (this controls the final vocabulary size)


#### BPE vs SentencePiece
* BPE marks word continuation
	* *Hello word@@ Id@@
	* Postprocessing: remove @@$<space>$ seqs
* Sentence Piece marks whitespace with an underscore for every following word
	* *Hello _wor ld*
	* Postprocessing: Deleta all spaces, then replace _ by space


#### Sentence piece
* Uses probabalistic model 
* Works slightly better than BPE


# Evaluation of machine translation
---

# Human evaluation
* Ultimately what we are interested in
* Very time consuming, costly
* Not reusable
* Subjective
### Adequacy
* Does the output convey the same meaning?
* Is part of message lost, distorted?
* Requires acces to either source or reference
### Fluency
* IS output good fluent english?
* Involves both grammatical correctness and idiomatic choices
* Can be judged by #toExpand 

### General translation quality
* Is sometimes difficult to distinguish between fluency errors and adequacy
* General translation quality is often used as a general measure of how good the translation is
* Perhaps from 1-5

# Automatic evaluation
* Cheap and re-usable
* Not necessarily reliable

### How
* Provide a human reference translation
* Compute similarity between reference translation and machine translation output

### The BLEU score
* The most popular (and most criticized) evaluation metric for MT
* Is meaningful for an entire corpus, not a single sentence
* Can technically add more references, but is usually not done
* Main idea: compute n-gram overlap (n=1..4) between system output and reference
	* Add a brevity penalty (for too short translations)
* $BLEU = min\left(1,\dfrac{Len_{Sys}}{Len_{Ref}}\right)\cdot Prec_q\cdot Prec_{2\cdot}Prec_{3\cdot}Prec_4$ #toExpand 
* ![[Pasted image 20231206004922.png | 500]]
* Problems:
	* Assumes that by having one single reference, you have the only translation
	* Ignores relevance of words
	* Does not account for morphology, typos, etc.
	* Operates on local level
	* Scores are meaningless
		* Can be very test specific, absolute 
	* Human translators score low on BLEU scores
* ![[Pasted image 20231206005121.png | 500]]

#### chrF: character-level score
* Break down words into character instead of ngrams
* Can improve BLEU


### BERTScore
* Produce sentence embedding of the system output
* Produce the sentence embedding of the reference
* Uses BERT to produce a cosine similarity score between the two
* Depends on the quality of the embedding model
* Unclear to what extent this accounts for differences in fluency


### Trained Metrics (e.g COMET)
* 15 years of MT evaluation campaigns have produced large datasets of human evaluations:
	* $<source, system_output,reference, score>$
* Use this dataset to train a classifier to predict scores
* If source, system_output, reference are encoded as sentence embeddings by a multilingual language model, the classifier can also be applied to languages not seen in training data

