
* **Lossless**: All info is preserved
* **Lossy**: Some info is lost
* Different compression methods compared (of RCV1): ![[Pasted image 20230913094624.png | 750]]

## Why compress?

* Less disk space
* Keep stuff in memory
* Increase speed of data transfer

## Vocabulary vs collection size

* In practice, vocabulary grows with collection
* **Heap's law**: *M = kT^b*
* _M_ is the size of the vocabulary, _T_ is the number of tokens in the collection
* Typical values: 30 ≤ k ≤ 100 and b ≈ 0.5
* In a log-log plot of vocabulary size M vs. T, Heaps’ law predicts a line with slope (stigningstall) about ½

![[Pasted image 20230913084205.png | 750]]_Heap's Law_


## Zipf's law
_The product of the frequency of a word f and its position in the frequency list (rank) r is constant_

* _f_ ∙ _r_ = _k_
* The first word is twice as frequent as the second, the first is three times as frequent as the third and so on
* The number of meaning of a word is correlated with it's frequency
* The length of a word is inversely correlated with it's frequency
* Words tend to clump together in a text
* cfi ∝ 1/i = K/i where K is a normalizing constant 
* cfi is **collection frequency**: the number of occurrences of the term ti in the collection

**The law only holds approximately**:
* Unstable behavior for most frequent words
* Large variation for least frequent words
* The constant (slope of the regression line) differs according to language and data type

### Consequences
* If most frequent term occurs cf_1 times:
	* the second occurs cd_1/2 times
	* The third occurs cf_1/3 times
![[Pasted image 20230913084648.png | 750]] _Zipf's law for Reuters RCV1_


## Compression for inverted indexes

#### Dictionary 
* Make it small enough to keep in main memory 
* Make it so small that you can keep some postings lists in main memory too 
#### Postings file(s) 
* Reduce disk space needed 
* Decrease time needed to read postings lists from disk 
* Large search engines keep a significant part of the postings in memory


# Dictionary compression
---

* Keep search in memory
* Embedded/mobile devices might have very little memory
* Search begins with dictionary, we want it to be small for a fast search startup time

## Dictionary storage

### Fixed width entries:
* All entries get the same space put off
* Wasteful
* Short words dominate token counts, but not type average

![[Pasted image 20230913085637.png | 500]]

### Dictionary as a string
* Store dictionary as a (long) string of characters
	* Pointer to next word shows end of current word
	* Hope to save up to 60% of dictionary space.
* Is more efficient than fixed width: from 11.2 MB to 7.6 MB

![[Pasted image 20230913085816.png | 500]]

### Blocking
* Store pointers to every kth term string
	* Example blow: k=4
* Need to store term length (1 extra byte)
* ![[Pasted image 20230913090033.png | 500]]

### Front coding
_Sorted words commonly have long common prefix - store differences only_

* When words share same prefix, add pointer for shared prefix and then multiple pointers for different variants

![[Pasted image 20230913090421.png | 500]]


# Postings compression
---
_Saves more space than dictionary compressions_

* Postings are much larger than dictionary, factor of at least 10
* Goal: Store each posting compactly

## Postings file entry

* Store list of docs containing a term in increasing order of docID
* Therefore we can write what the difference between an entry and the previous, giving us smaller numbers to store
* Consequences: it suffices to store gaps (differential encoding)
* Hope: Most gaps can be encoded/stored with far fewer than 20 bits

## Variable length encoding
_Use different encoding based on frequency_

### Variable Byte codes (VB)
* If a docID is more than one byte add a 0 at the start of the byte, add one in the last byte
* If the average gap for a term is _G_, we want to use ~log_2 G bits/gap entry
* If *G* ≤127, binary-encode it in the 7 available bits and set c =1
* Else encode G’s lower-order 7 bits and then use additional bytes to encode the higher order bits using the same algorithm 
* At the end set the continuation bit of the last byte to 1 (c =1) – and for the other bytes c = 0
![[Pasted image 20230913093308.png | 500]]
![[Pasted image 20230913093420.png | 500]]

### Other variable unit codes
* Instead of bytes we could use different units of alignment, fex 32 bits (words), 16 bits, 4 bits (nibbles)
* Nibbles wastes less space for many small gaps

## Unary code

* Represent _n_ as _n_ 1s with a final 0
* Unary code for 3 is 1110
* Unary code for 40 is 11111111111111111111111111111111111111110
* Is not very efficient, but can be efficient when used with Gamma codes

## Gamma codes

* Is usually not used in practice
* Compressing and manipulating at the granularity of bits can be slow
* Variable byte encoding is aligned and therefore potentially more efficient
### How
* Represent a gap _G_ as a pair _length_ and _offset_(offset is G in binary but with leading bit cut off)
	* 13 -> 1101 -> 101
* length is the length of offset
	* 13 (offset 101) -> 3
* Encode length with unary code 1110
* Gamma code of 13 is the concatenation of length and offset 1110101
* Gamma code examples:![[Pasted image 20230913094223.png | 500]] 

### Properties
* All gamma codes have odd number of bits
* _G_ is encoded using 2 ⎣log G⎦ + 1 bits
* Almost within a foctor of 2 of best possible log_2 _G_


# Gamma and Delta coding
#toExpand 

# Simple9 (S9) coding
_Produce a word-aligned code, try to pack several numbers into one word_

* Each word is split into 4 control bits and 28 data bits
* Store and retrive numbers using fixed bit masks

## Algorithm
* do the next 28 numbers fit into one bit each? 
	* if yes: use that case 
	* if no: do the next 14 numbers fit into 2 bits each? 
		* if yes: use that case 
		* if no: do the next 9 numbers fit into 3 bits each?
			* … and so on …
#toExpand 


# PFOR-DELTA
_Compress/decompress many values at a time_

* Compress differently based on chunks of data
* Good compromise: choose size such that 90% fit, code the other 10% as exceptions
* Exceptions stored at the end as ints, (using 4 bytes each)
* Exceptions (gray) are linked lists within the locations (3 means 'next exception 3 away') ![[Pasted image 20230913100420.png | 750]]

## Rice coding


## Golomb encoding