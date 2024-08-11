
# Jaccard coefficient
*A way to measure overlap between two n-grams*

* Returns a number between 0 and 1
* ![[Pasted image 20230912123814.png | 500]]
#Useful?

# Soundex
_Class of heuristics to expand a query into phonetic equivalents_

* Language specific 
* Mainly for names 
* E.g., chebyshev → tchebychef
* Algorithms makes a hashcode of a word and queries and compares values
* Not very useful, but can be good for high recall tasks

## Typical algorithm
1. Turn every token to be indexed into a 4-character reduced form 
2. Do the same with query terms 
3. Build and search an index on the reduced form

# Example
1. Retain the first letter of the word. 
2. Change all occurrences of the following letters to '0' (zero): 'A', E', 'I', 'O', 'U', 'H', 'W', 'Y'. 
3. Change letters to digits as follows: 
	* B, F, P, V → 1 
	* C, G, J, K, Q, S, X, Z → 2 
	* D,T → 3 
	* L → 4 
	* M, N → 5 
	* R → 6 Sec. 3.4 43 Introduction to Information Retrieval Soundex continued 
4. Remove all pairs of consecutive digits. 
5. Remove all zeros from the resulting string. 
6. Pad the resulting string with trailing zeros and return the first four positions, which will be of the form .
* 'Herman' will become H655

# Index construction
---
## Hardware basics
* Design decisions in information retrieval are based on hardware
* Memory vs disk access
* Disk seek
* Cache misses
* Block sizes and cache
* Fault tolerance, better to use many regular machines rather than one fault tolerant machine

### Notation for lecture:
![[Pasted image 20230906113906.png | 500]]

## Constructing an index:

* Documents are parsed to extract words and these are saved with the Document ID.
* After all documents have been parsed, the inverted file is sorted by terms.
* In-memory index construction does not scale, 

### Problems
* Memory management

## Blocked sort-based Indexing
_Parse into multiple blocks, more memory friendly_

* Accumulate postings for each block (blocksize so it can fit into main memory)
* Tokenize
* Sort, write to disk
* Merge blocks into on long sorted order

![[Pasted image 20230906114411.png | 500]]


## Single-pass in-memory indexing

* Usually used when you can fit everything in main memory #Maybe
* Key idea 1: Generate separate dictionaries for each block – no need to maintain term-termID mapping across blocks. 
* 
* Key idea 2: Don’t sort. Accumulate postings in postings lists as they occur. 
* With these two ideas we can generate a complete inverted index for each block. 
* These separate indexes can then be merged into one big index.
* Can be more efficient with compression


# Distributed indexing
---
*  Used for web scale indexing, using large distributed systems

## MapReduce

* Maintaining a **master machine**  directing the indexing job is considered more safe
* Break up indexing into sets of parallel tasks
* Master machine assigns each task to an idle machine from a pool
* Split documents into **splits** (subset of documnets corresponding to blocks)
* Can also be used for statistics and other uses

### Parsers
* Master assigns split to idle parser machines
* Parser reads document at a time and emits (term, doc) pairs
* Writes pairs into j partitions

### Inverters
* collects all (term, doc) pairs


### Data flow:

![[Pasted image 20230906115417.png | 500]]

x
# Dynamic indexing
---
* Up to now we have assumed collections are static, not realistic
* This means postings and dictionaries have to be dynamic

## Simple approach
* Maintain big main index
* New docs to into small auxiliary index
* Search across both, merge results
* Deletions #todo
* Periodically re-index into one main index

### Problems
* 

## Uptime
* If a non-fault-tolerant system with 1000 nodes, each node has 99.9% up-time, what is the up-time of the system? 
* Answer: 63%

