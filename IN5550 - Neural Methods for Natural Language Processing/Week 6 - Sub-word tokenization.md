
# Why
---

* In models like [[Week 6 - word2vec embeddings|word2vec]], we use the whole word as a token. In these models there is a big problem with out-of-vocabulary words. This can be fixed by using sub-word tokenization
* Smaller vocabularies
* No modern models uses full words anymore
* ![[Pasted image 20240226135938.png|400]]


# Byte-pair encoding
---

* Originally algorithm for text compression, now used as tokenization techniques behind most language models, including **GPT**s
* Algorithm for creating a set of subwords from a corpus
* Usually **pre-tokenization** is performed first (Typical tokenization)
* Letters are not good atomic unit, instead `UTF-8 bytes` are used, as they have a smaller number of characters


## Example

* Text corpus $C=AABCCAABAABCC$
* Initial subwords:
	* $s_0=$"$A$"
	* $s_1=$"$B$"
	* $s_2=$"$C$"
* Now we can encode $C$ into: "$0012200100122$"
1.  Look at the training corpora, find the most common combination of subwords, in our case it can be "$01$", or "$AB$", so we can create a new subword $s_0=$"$AB$"
2. Replace the initial encoding to support new vocabulary: "$0322030322$"
3. Repeat `1.` until enough, in our example the next subword could be "$03$", or "$AAB$"
* Continue until dictionary is of chosen size