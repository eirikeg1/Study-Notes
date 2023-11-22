
# Ranked Retrieval
---
_In contrast to Boolean Retrieval, Ranked Retrieval gives a score instead of either matching or not_

* Boolean retrieval makes crafting good queries much more important
* Boolean is good for experts or applications which use specific queries
* Ranked is better for the majority of users
* Number of results is not a problem in Ranked Retrieval, as you can sort by relevance


## Scoring
* Assess score and keep track of the best ones, then we don't need to sort all the results afterwards

**One-term-query:**
* If the query term does not occur in the document score should be 0
* The more frequent the query term, the higher score

### Jaccard coefficient

* Commonly used measure of overlap of two sets A and B
* Example:
* Jaccard(A,B) = |A ∩ B| / |A ∪ B| 
* Jaccard(A,A) = 1 
* Jaccard(A,B) = 0 if A ∩ B = 0 
* A and B don’t have to be the same size. 
* Always assigns a number between 0 and 1.

#### Problems with Jaccard for scoring
* Doesn't consider term frequency
* Rare terms in a collection are more informative than frequent terms, Jaccard doesn't consider this
* Later in this lecture, we’ll use § . . . instead of |A ∩ B|/|A ∪ B| (Jaccard) for length normalization. 


## Term document count matrices

* Consider number if occurences of a term in a document
* Each document is a count vector for each term
* ![[Pasted image 20230913103229.png | 750]]
### Term frequency *
* $tf_{t,d}$* of term _t_ in document _d_ is the number of times _t_ is in _d_
* If a word appears 10 times more than another it does not mean it is 10 times less relevant, therefore we use log

### Log frequency weighting
* Log frequency weight of term t in d is ![[Pasted image 20230913103525.png | 500]]
* 0 → 0, 1 → 1, 2 → 1.3, 10 → 2, 1000 → 4,...
* Score: ![[Pasted image 20230913103608.png | 350]]

### Document frequencies
* *df_t*
* Rare terms are more informative than frequent terms (recall stop words)
	* We should consider this for the weight

#### idf weight
* **inverse document frequency** of t is: ![[Pasted image 20230913103901.png | 250]]
* Usually we use log (N/df_t) to "dampen" the effect of idf
* Does not effect one term queries, but weights the terms in the query in relation to each other
	![[Pasted image 20230913103952.png | 500]]

#### Collection vs document frequency
* Collection frequency of t is the number of occurrences of t in the collection, counting multiple occurrences
* ![[Pasted image 20230913104253.png | 500]]

### tf-idf weighting

* Adds the term frequency
* Popular
* Increases with number of occurrences within a document
* Many variants, with or without logs, document lengths, weighing query terms,...
* $w = log(1+log(tf))*log_{10}(N/df)$
* ![[Pasted image 20230913104505.png | 500]]
* ![[Pasted image 20230913104718.png | 750]]
#### Example variant of tf-idf
   ![[Pasted image 20230913110548.png | 500]]

# Representation as vectors
---
## Documents as vectors
* We have a $|V|$-dimensional vector space
* Terms are axes of the space
* Documents are points or vectors in this space
* Very height-dimensional: tens of millions of dimension when applied to web search
* Very sparse vectors, most are 0

## Queries as vectors
* **Key idea 1**: Do the same for queries: represent them as vectors in the space
* **Key idea 2**: Rank documents according to their proximity to the query in this space
* proximity = similarity of vectors 
* proximity ≈ inverse of distance

### Length normalization
* Vector can be normalized by dividing each component by length ($L_2$ norm): ![[Pasted image 20230913105705.png | 350]]

## Formalizing vector space ranking/proximity
* Represent the query as a weighted tf-idf vector 
* Represent each document as a weighted tf-idf vector 
* Compute the cosine similarity score for the query vector and each document vector 
* Rank documents with respect to the query by score 
* Return the top K (e.g., $K = 10$) to the use

### Euclidean distance
* Works, but is larger for longer vectors so not very good

### Cosine distance
* Cosine is a monotonically decreasing function for the interval [0, 180] degrees
* Can be used to look at the difference between two vector directions
* ![[Pasted image 20230913105534.png | 350]]

### Cosine(query,document)

* $q_i$ is the tf-idf weight of term i in the query 
* $d_i$ is the tf-idf weight of term i in the document
* is the cosine similarity of $q_i$ and $d_i$
* Formula for non-normalized vectors: ![[Pasted image 20230913110105.png | 500]]
* For length-normalized vectors, cosine similarity is the dot product: ![[Pasted image 20230913105946.png | 500]]

#### Example implementation
   ![[Pasted image 20230913110443.png | 500]]
#### Example: compute scores with cos(q,d)
   ![[Pasted image 20230913110333.png | 500]]









