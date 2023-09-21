
# Efficient cosine ranking
---
* Find the K docs in the collection “nearest” to the query  -> K largest query-doc cosines. 
* Efficient ranking: 
	* Computing a single cosine efficiently. 
	* Choosing the K largest cosine values efficiently. 
	* Can we do this without computing all N cosines

## Cosine similarity is only a proxy
* User has a task and a query formulation
* Cosine matches docs to query 
* Thus cosine is anyway a proxy for user happiness

## Use heap for selecting top K
* Binary tree in which each node’s value > the values of children 
* Takes $2J$ operations to construct, then each of K “winners” read off in $2log(J)$ steps. 
* For $J=1M, K=100 $, this is about 10% of the cost of sorting


## Index elimination
* Basic cosine computation algorithm only considers docs containing at least query
* Can be taken further:
	* Only consider high-idf query terms
	* Only consider docs containing many query terms
* Example of high-idf query terms only:
	* For a query such as *catcher in the rye* 
	* Only accumulate scores from *catcher* and *rye*


## DAAT - Docs containing many query terms
#toExpand 
* Any doc with at least one query term is a candidate for the top K output list
* For multi-term queries, only compute scores for docs containing several of the query terms 
	* Say, at least 3 out of 4
* Easy to implement in postings traversal

## Champion lists
*Precompute for each dictionary term t, the r docs of highest weight in t’s postings*

* Call this the **champion list** for $t$
* Note that _r_ has to be chosen at index build time, so it's possible that $r>k$
* At query time, only compute scores for docs in the champion list of some query term


## Static quality score
*We want top-ranking documents to be both relevant and authoritative*

* Relevance is being modeled by cosine scores 
* Authority is typically a query-independent property of a document
* Examples of authority signals:
	* Wikipedia among websites 
	* Articles in certain newspapers 
	* A paper with many citations 
	* Many bitly’s, likes or social referrals marks 
	* (Pagerank)


## Net score
*combination of cosine relevance and authority*

* Typically sort k first of docs by net score
* Example implementation: $net-score(q,d) = g(d) + cosine(q,d)$
	* Can use other linear combinations
	* Formula can be calculated with machine learning


### Net score - fast methods

**First idea: Order all postings by g(d)**
* Thus, can concurrently traverse query terms’ postings for postings intersection and cosine score computation
* Under g(d)-ordering, top-scoring docs likely to appear early in postings traversal
	* In time bound applications even if the search must terminate early the results should be good


## High and low lists
_A means for segmenting indexes into two tiers_

* For each term, we maintain two postings lists called high and low (high like champion list)
* When traversing postings on a query, only traverse high lists first 
	* If we get more than K docs, select the top K and stop 
	* Else proceed to get docs from the low list


## Impact-ordered postings
*compute score for docs which wf_t,d is high enough*

* Sort postings list by wf
* All postings are not in a common order

#### Document at a time:

#toExpand 
## Early termination
_Stop traversing when result is good enough_


## idf-ordered terms
#toExpand 

## Cluster pruning
*Consider less documents at a time*

* Split documents into clusters based on documents and only search that cluster
#toExpand 

### Preprocessing
* Pick $\sqrt{N}$ docs at random, called leaders
* For every other doc, pre-compute nearest leader
* Docs attached to a leader: its followers
* Likely: each leader has ~$\sqrt{N}$ followers

### Query processing
* Given query Q, find nearest leader
* Seek K nearest docs from among L's followers

## Parametric and zone indexes
* Use metadata like for example author, title, language or format
* Can be used for filtering down search space

## Zone
* Region of doc which can contain text (abstract, main content, intro)
* Build inverted indexes as well on zones
* Allows us to differenciate if a word is in the abstract or in references
* Can either create a separate postings list for each zone, or have multiple postings in one postings list, based on what quereies you want



