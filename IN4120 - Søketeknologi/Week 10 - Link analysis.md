

* Look at references between documents (for example link from one webpage to another)
* Can be out of control of page owners #Maybe 
* Can be represented as a graph problem
* Can be made with crawlers
* For example assumption: Good nodes don't point to bad nodes
* ![[Pasted image 20231025105535.png|500]]
* ![[Pasted image 20231025105558.png|500]]

## Anchor text
* Can be enough to look at the anchor text when considering a page
* For example when searching for *IBM* you need to distinguish between:
	* IBM’s home page (mostly graphical)
	* IBM’s copyright page (high term freq. for ‘ibm’) 
	* Rival’s spam page (arbitrarily high term freq.)
* ![[Pasted image 20231025110233.png | 500]]

## Citation analysis
* Bibliographic coupling frequency 
	* Articles that co-cite the same articles are related
* Citation indexing
	* Who is this author cited by? (Garfield 1972)

# Pagerank scoring
_Algorithm made by Larry Page which ranks pages based on how many links going into it and quality of linkers_
* Technique:
	1. Start at a random page
	2. At each step, go out of the current page along one of the links on that page, equiprobably
* In the long run, each page has a long-term visit rate, this is the score
* Often used in web search engines, but is rarly the full story of ranking
* Visit rate can be computed with Markov chains

## Summary
* Preprocessing: 
	* Given graph of links, build matrix P. 
	* From it compute a – left eigenvector of P. 
	* The entry ai is a number between 0 and 1: the pagerank of page i. 
* Query processing: 
	* Retrieve pages meeting query. 
	* Rank them by their pagerank. 
	* But this rank order is query-independent …

## Markov chains
* Consists of $n$ states (nodes). Plus an $n\cdot n$ transition probability matrix $P$
* At each step we are in one of the states
* If the Markov chain is **ergodic**, there is an unique long-term visit rate for each state
	* Every node is reachable from one node to any other over a given period of time
* Probability vector says where we are: (000…1…000)
* ![[Pasted image 20231025111546.png | 500]]

## Dealing with dead ends
* Can be done by jumping to a random web page
* Sometimes also teleport from non-dead end pages, for example 10% of the time


# Hyperlink Induces Topic Search (HITS)
#toExpand 
* Instead of ordered list of pages each meeting the query, find two sets of interrelated pages
* Hubs are good lists of links, authority pages occur recurrently on good hubs for the subject
* Finding base set:
	* Start with a base set of pages that could be good hubs or authorities
	* From these, identify a small sets of top hub and authority pages
	* Given text query, use a text index that get all pages containing browser (call this the *Root set*)
	* Add any pages which either:
		* Points tot a page in root set
		* is pointed to by  a page in the root set
	* This is the *base set*
* 


# Technical connectivity
---

## Adjacency lists


## Gap encoding


