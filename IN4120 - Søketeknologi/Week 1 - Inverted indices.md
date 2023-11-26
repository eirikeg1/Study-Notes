## Information Retrieval
* Is used in finding material of an unstructured nature that satisfies an information need from within large collections (usually documents of texts stored on computers)
* Examples are:
	* Email search
	* Searching laptop
	* Corporate knowledge bases
	* Legal information retrieval

![[Pasted image 20230823125317.png | 500]]
## Measuring accuracy
* **Precision** is the fraction of retrieved docs that are relevant to the user's information need
* **Recall** is the fraction of relevant docs in collection which are retrieved

## Incidence vectors
* Store a matrix with documents and terms. 1 if document contains term else 0
* Very inefficient, slow for big datasets
* Sparse entries as most documents usually don't contain all terms possible (often all words in language)
## Inverted Index
* Identify each document with a **docID** (document ID)
* Store the terms in a map structure, where the values is a list (usually a linked list) of all the documents containing it.
* The values can be in any type of collection, but linked lists are usually used as they are memory efficient when the entries has a lot of different sizes. The most important part is that the values are **sorted by docID**
* 

![[Pasted image 20230823134837.png]]

### Inverted Index construction
![[Pasted image 20230823135133.png |500]]

* **Tokenization** is to cut character sequence into smaller words, challenges are splitting words like _John's_
* **Normalization** is to map text and query term to the same form for example making **U.S.A** and **USA** match.
* **Stemming** is to make different forms of root to match, for example **authorize** and **authorization**.
* **Stop words** is words which is common to omit words like **the, a, to, of**
* **Term** is a word or phrase as stored in the posting
* 

### Indexer steps:
* **Sort** by terms, and docID
* **Dictionary & Postings** is the step where we create the dictionary and linked list of all the common entries.
* Add document frequency in dictionary

### Storage
* This is much more efficient than with **Incident vectors** since instead of storing a sparsely filled out matrix of term-count times document-count we only store a dictionary with term-count keys and values for the matching documents.
* Therefore we only store the values we need. As well as the pointers in the dictionary and linked lists.

## Information Retrieval Techniques
---
#### Boolean retrieval: Exact match
_The **Boolean retrieval model** is being able to ask a query that is a Boolean expression_
* Using AND, OR and NOT to join query terms
* Views each document as a **set** of words
* Is precise: Document matches condition or not
* Is the primary commercial retrieval tools for 3 decades
* Many search systems uses Boolean, for example email, library catalogue and Mac OS spotlight search
#### Query processing: AND
* For example if we are processing the query **Brutus** and **Caesar**:
	1. Locate **Brutus** in the dictionary and retrieve it's postings
	2. Locate **Caesar** in the dictionary and retrieve it's postings
	3. Find the intersect between the two postings (The common postings entries)

	**Simple algorithm for finding the intersect**:
		1. Start at the start of both postings and compare the values (docIDs)
		2. If the values are different, iterate once on the smallest docID. If the values are the same add the docID to the return array and iterate on both.
		3.  If not on the end of a posting go back to 1. 

#### Query optimization
_Consider a query that is an AND of n terms_
* When doing multiple Boolean operations you can only compare two at a time. 
* In order to optimize it is usually better to do the operations on the entries with the smallest frequencies first.

### Phrase queries
_If you want to search for matches for exact phrases, for example "stanford university" (word by word) it is no longer enough to only store  \<term : docs> entries_

#### Biword indices
* One way is to make entries for biwords (word pairs). 
* For example the text "Friends, Romans, Countrymen" would generate the biwords "friends romans" and "romans countrymen".
* This makes two-word phrase query processing immediate.
* Longer phrases can be broken down as a Boolean query on the biwords.
* Can give false positives

#### Positional index
_Store the positions of the term in the document, in the postings (with the docID)_
* When merging recursively look for docs where indexes match search
* Is substantially larger, usually 2-4 times more storage
* _LIMIT! /3 STATUTE /3 FEDERAL /2 TORT_ is a query where /k means _within k words of_
* ![[Pasted image 20230830103257.png | 500]]
* 

#### Combination schemes
* It is normal to combine Biword and positional
* For particular phrases (“Michael Jackson”, “Britney Spears”) it is inefficient to keep on merging positional postings list. Just add them as one entry

# Precision and Recall
---
**Precision** 
* How many of the accurate predictions did we find?
* true positives / (true positives + false positives)
* $\dfrac{TP}{TP+FP}$

**Recall**
* How accurate predictions
* $\dfrac{TP}{TP + FN}$

![[Pasted image 20230829151827.png | 500]]
