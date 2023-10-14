
## Evaluation metrics
* How fast does it index?
* How fast does it search?
* Does it recommend good similar products?
* Relevant results?
* Results get clicked a lot?
	* But is it misleading?
* Users buy after search?
* Repeat visitors?

# Benchmarks
---
## Measuring the relevance of search results
* Three elements: 
	1. A benchmark document collection 
	2. A benchmark suite of queries python
	3. An assessment of either **Relevant** or **Non-relevant** for each query and each document
* Binary vs more nuanced relevance
* When outsourcing to multiple crowd-sourcing platforms, the variance between judgments will be very high

## Evaluating IR system
* Translate user need to query
* relevance assessed based on user need, not query

## Rank based measures
* Binary relevance 
	* Precision@K (P@K) 
	 * Mean Average Precision (MAP) 
	 * Mean Reciprocal Rank (MRR) 
 * Multiple levels of relevance 
	 * Normalised Discounted Cumulative Gain (NDCG


### Precision@K (P@K)
* Rank threshold _K_
* Compute % relevant in top _K_
* ignores docs below _K_
![[Pasted image 20230927112018.png | 500]]

### Precision recall curve
* Red is **interpolated** precision recall
![[Pasted image 20230927112108.png | 500]]

### Mean Average Precision
* Average precision across multiple queries/rankings
* Compute Precision@K for each K, use this average
* If relevant document is never retrived, assume precision to be zero
* Requires many relevance judgements in text collection
* MAP is macro-averaging: each query counts equally
* Consider rank position of each relevant doc
	* $K_1, K_2, K_3, ... K_R$
* ![[Pasted image 20230927112603.png | 500]]

## Discounted Cumulative Gain
*Popular measure for evaluating web search and related tasks* 

* Two assumptions: 
	* Highly relevant documents are more useful than marginally relevant documents 
	* the lower the ranked position of a relevant document, the less useful it is for the user, since it is less likely to be examined
* Uses **graded relevance** as a measure of usefulness, or gain, from examining a document
* Gain is accumulated starting at the top of the ranking and may be reduced, or discounted, at lower ranks
* Typical discount is $1/log(rank)$
* ![[Pasted image 20230927113440.png | 500]]


### Normalized Discounted Cumulative gain at rank _k_

* Normalize DCG at rank n by the DCG value at rank n of the ideal ranking 
* The ideal ranking would first return the documents with the highest relevance level, then the next highest relevance level, etc
* Useful for contrasting queries with varying numbers of relevant results


## Mean Reciprocal Rank
_Rank posision K, of first relevant doc_

* MRR is the mean RR across queries

## Human judgements
* Expensive 
* Inconsistent 
	* Between raters 
	* Over time 
* Decay in value as documents/query mix evolves 
* Not always representative of “real users
* Set patterns, not necessarily because of actual relevancy


# Assessment methodology
---
## User clicks
* Pattern, but strong posision bias so unreliable
![[Pasted image 20230927114108.png | 500]]

![[Pasted image 20230927114440.png | 500]]

### Pairwise relative rankings
* Pairs of the form: DocA better than DocB for a query
* Given a set of pairwise preferences P 
* We want to measure two rankings A and B 
* Define a proximity measure between A and P

#### Kendall tau distance
* X = number of agreements between a ranking
* Y = num of disagreements
* KT distance = (X-Y)/(X+Y)
* Example:
	![[Pasted image 20230927114810.png | 500]]

## Critique of additive relevance
* Doc can be redundant while highly relevant
* Marginal relevance if better for utility for user
* Pushes us to assess a slate of results, rather than to sum relevance over individually assessed results

## Facts/entities
_Sometimes good with no clicks?_
![[Pasted image 20230927115235.png | 500]]


## A/B testing
* Test a single innovation
* 
