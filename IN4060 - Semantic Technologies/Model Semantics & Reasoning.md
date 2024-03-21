
* Builds on [[RDF- and RDFS-semantics#Triples vs Description Logic syntax|Description Logic syntax]] as in [[RDF- and RDFS-semantics]]

## Literal semantics
* #toExpand 

## Blank Node semantics
* 

## Properties of Entailment by Model Semantics

### Monotonicity
_If a rule applies for the domain, it applies for all new elements later added_
* Assume $A \vDash B$
* Then add info to $A$, e.g. $A' \supseteq B$
* Then $B$ is still entailed: $A' \supseteq B$
* **RDF/RDFS** is monotonic #Maybe

## Entailment and Derivability

* Two different notions
* In contrary to knowledge base lookups, if something entails something, it holds for all future values, not the case with database lookups
* Should correspond $A \vDash B \text{ iff } B$ can be derived from $A$

### Entailment
_Closely related to the meaning of things_
* Higher confidence than in a bunch of rules
* Semantics given by the standard, rules are just informative
* Can't directly check mechanically/manually

### Derivability
_Can be checked manually_
* Forward or backward chaining

### Soundness
_The calculus gives no wrong answers_
* Two directions
	* If $A \vDash B$, then $B$ can be derived from $A$
	* If $B$ can be derived from $A$, then $A \vDash B$
* 2nd is usually more important
* If calculus says something is entailed, it is really entailed
* Has to be (manually) checked

![[Pasted image 20240306135049.png|350]]

### Completeness
_Any entailment can be found using the rules_
* Two directions:
	* If $A \vDash B$, then $B$ can be derived from $A$
	* If $B$ can be derived from $A$, then $A \vDash B$
* Something is complete if it has enough rules, as all rules in an $I$ might not be enough
* Cant be checked separately for each rule, only for whole rule set
* ![[Pasted image 20240306135622.png|350]]


### Closed World Assumption
_If a thing is not listed in the knowledge base, it does not exist_
* If its not stated or derivable, its false

### Open World Assumption
_There might be things not mentioned in the knowledge base_
* If new data breaks, add new rules #toExpand 
* Better for semantic web

### Two kinds of consequence

* It should in theory be possible to mix (one )
#### RDFS rules
![[Pasted image 20240306134219.png|400]]

#### Model semantics
![[Pasted image 20240306134245.png|400]]
