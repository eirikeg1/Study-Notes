

# Global Methods
---
* 
## Query expansion

* used to improve recall
* e.g search for _laptop_, but also get results for Dells' _notebooks_
* 

# Local methods
---

# Relevance Feedback

* User gives feedback on results so we can tune the query
* No clear evidence it a more effective use of user time

## Direct/Indirect relevance feedback

* Can be a problem to only use clicks as scoring function, as then you rank on the same which you show
* _infinite loop_ of users clicking because it is shown at the top
* Scoring does not necessarily have to be user or query specific

## Ad hoc retrieval
#toExpand 
* an instance of relevance feedback
* Give a suggestion for similar result for entries #Maybe 
* Imagine the 3d space below, when a user clicks a result the search space changes to a space between the search and the result #Maybe 

* ![[Pasted image 20231004103503.png | 500]]
* ![[Pasted image 20231004103605.png | 500]]


## Centroid

* The center of a mass of points
* $C$ is a set of documents
* ![[Pasted image 20231004103719.png | 350]]


## Rocchio Algorithm

* Try to find the query which maximizes the query and the relevant ones minus the non relevant ones
* Finds the _centroid_ of the known most relevant documents:
* ![[Pasted image 20231004104453.png | 500]]
* Tries to separate relevant and non relevant
* ![[Pasted image 20231004103853.png | 500]]
* ![[Pasted image 20231004103915.png | 500]]
* Usually better to add beta and gamma values :
	* $D_r$ is set of known docs
	* $q_m$ is the modified query vector
	* Weights are hand chosen or set empirically
* ![[Pasted image 20231004104011.png]]
* 


# Pseudo relevance feedback

* Can often work very well
* Can go horribly wrong


# Query assist

* Auto complete suggestions
* ![[Pasted image 20231004105143.png | 350]]
* You can use a manual thesaurus to find similar words/synonyms and more
	* or each term $t$, expand query with synonyms and relevant words
	* May make queries less original
	* Words like _Jaguar_ and _car_ might be classified as differen
* **Global Analysis**: Global Analysis on collection
* **Local analysis**, analayse docs in results

### Automatic Thesaurus expansion

* Attempt to generate a thesaurus automatically by analysing the collection of documents
* Can be based on co-occurence in a co-occurence thesaurus
	* Word embeddings
