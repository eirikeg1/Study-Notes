
* There are two types of semantics for e.g. programming languages **declarative**, **operational**


# Formal semantics
---
#toExpand

* Study of how to model the meaning of a **logical calculus**
* **logical calculus** consists of:
	* finite set of symbols
	* grammar, specifies formulae
	* set of axioms and inference rules from which we construct proofs
* A logical calculus can be defined apart from any interpretation. 
* A calculus that has not been furnished with a formal semantics

## Abstractions
_Logical calculus abstracts 'the real word'_

![[Pasted image 20240228125537.png|350]]


# Short forms
---
_'Description Logic' syntax_

* Resources and Triples are no longer all alike
* No need to use the same general triple notation
* Is used much in particular for **OWL**
* Use alternate notation:
	![[Pasted image 20240228132641.png|350]]


## Triples vs Description Logic syntax

* Relations are sets of tuples
  
	![[Pasted image 20240228133116.png|350]]
	![[Pasted image 20240228133130.png|350]]


## Interpretations

* A DL interpretation $I$ consists of:
	* A set $\Delta^I$ called the domain of $I$
* for each individual URI, an element $i^{I}\in\Delta^I$
* For each class URI, a subset $C^{I}\subseteq\Delta^{I}$
* Each property URI $r$, a relation $r^I\subseteq\Delta^{I}\times\Delta^{I}$
* Just because the names **URI**s look familiar, they don't have to denote what we think, there is no way to ensure it does

### Example

	![[Pasted image 20240228133930.png|350]]
