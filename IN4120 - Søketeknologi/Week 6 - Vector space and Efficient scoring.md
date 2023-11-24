
![[Pasted image 20230927103054.png | 700]]
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
* For $J=1M, K=100$, this is about 10% of the cost of sorting


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
* Is usually better for complicated queries, compared to **TAAT**, but is usually more expensive, especially for large corpora


## Champion lists
*Precompute for each dictionary term t, the r docs of highest weight in t’s postings*

* Call this the **champion list** for $t$
* Note that _r_ has to be chosen at index build time, so it's possible that $r>k$
* At query time, only compute scores for docs in the champion list of some query term
* Improves efficiency of query processing
* Gives bigger benefits in large-scale search systems
* Usually used with **TAAT**


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
	* *wf* is the weighted frequency of you choice (for example tf_idf)
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
* Pick k random leaders, docs follows their closest leader
* Best leader and his followers are docs which are considered #Maybe 
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
* Can add metadata to postings

## Zone
* Region of doc which can contain text (abstract, main content, intro)
* Build inverted indexes as well on zones
* Allows us to differenciate if a word is in the abstract or in references
* Can either create a separate postings list for each zone, or have multiple postings in one postings list, based on what queries you want

## Query term proximity
* What is the proximity of word in a certain window size?
* Let w be the smallest window in a doc containing all query terms, e.g., 
* For the query strained mercy the smallest window in the doc *The quality* of mercy is not strained is 4 (words

## Query parsers
* Spawn one or more queries to indexes:
	* #toExpand 

## Aggregate scores
* Score functions combining cosine, static quality, proximity, etc.
* Some applications combine using expert tuning
* More common with machine learning

## TAAT - _Term At A Time_
* Scores for all docs computed concurrently, one query term at a time

## DAAT - _Document At A Time_
* Total score for each doc (incl query terms) computed, before proceeding
* Does not have intermediate and partial scores lit _TAAT_

# Safe vs non-safe ranking
---
_Safe guarantee that K docs returned are the K absolute highest scoring docs_

## Safe ranking

## WAND Scoring
#toExpand 
* How often is each term in doc?
* Give an **upper bound** for each term before comparing
* Have a **threshold** we compare with the **upper bound**, to decide if we should evaluate doc
* When comparing documents have a cursor on its own document and term, calculate one term and use the **upper bound** to decide if you should continue to evaluate the doc
* **DAAT** approach
## Static quality scores

* **Relevance** is being modeled by cosine scores 
* Authority is typically a query-independent property of a document

Examples:
* Wikipedia among websites
* Articles by trusted sources

