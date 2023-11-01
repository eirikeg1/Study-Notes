
# Bloom Filter

* Probabilistic data structure for checking set membership
	* No means no, yes means probably
* Bit vector with $m$ bits, and $k$ independent hash functions, used to store $n$ member values


## Bit-signature indices

* Signature: sequence of bits in bloom filter, representing set of terms in string
* Instead of using bit vectors for docs and terms, use a matrix with docs and bloom filter of terms
	* Saves a lot of space
* Cost of false positives 'negligible' for websearch, as results doesn't need to be correct and results are ranked
* Plenty of other engineering tricks involved 
	* E.g., frequency-conscious signatures, higher rank rows, sharding by document length, ...
* 