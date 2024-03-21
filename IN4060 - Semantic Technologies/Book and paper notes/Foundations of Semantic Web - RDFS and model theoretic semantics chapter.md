

* **Grounded triple**: Triple not containing blank nodes, all parts of triple must be in vocabulary and correspond to the interpretation
* **Ill-typed** and **well-typed**: A **rdf:XMLLiteral** in [[#RDF-Interpretations]] is **well-typed** if it satisfies the syntactic conditions for being contained in the lexical space of **rdf:XMLLiteral**, otherwise it is **ill-typed**
	* **Well-typed** are mapped to literal values (**LV**), while **ill-typed** are mapped to **resources** that are not literal values.



# Interpretations
---

## Simple-Interpretations

### Contains
_Simple interpretation $\mathcal{I}$ of given vocabulary $V$_

* **IR**: non empty set of [[Jena - Java library for RDF#Resources|resources]], alternatively called domain or universe of discourse of $\mathcal{I}$
* **IP**: The set of [[Mathematical foundations#Properties|properties]] of $\mathcal{I}$ (may overlap with **IR**)
* **$I_{EXT}$**: a function assigning to each property a set of pairs from **IR**
	* i.e. $I_{EXT}:IP\rightarrow 2^{IR\times IR}$, where $I_{EXT}(p)$ is called the extension of the property $p$
* $I_{s}$: a function assigning to each property a set of pairs from **IR** and **IP**
	* i.e. $I_{s}: V\rightarrow IR\cup IP$
* $I_{L}$: a function from the typed literals from $V$ into the set of **IR** of resources
* **LV**: a particular subset of **IR**, called the set of **literal values**, containing at least all untyped literals from $V$

## RDF-Interpretations
_RDF-interpretation of vocabulary V is a simple-interpretation that additionally satisfies a few extra conditions_

### Extra conditions
_Additional conditions on top of the simple-interpretations'_

* $x\in IP$ exactly if: $\langle{x,\text{rdf:Property}^{\mathcal{I}}\in I_{EXT}(\text{rdf:type}^{\mathcal{I}})}\rangle$
	* $x$ is a property exactly if it is connected to the resource denoted by **rdf:Property** via the **rdf:type**-property (automatically causes $IP\subseteq IR$ for any RDF-interpretation)
* Other conditions... #NotImportant

### Contains
_Everything in simple-interpretations, plus..._

* **$V_{RDF}$**: set of [[RDF Overview#URIs|URIs]]
	* i.e. **rdf:type**, **rdf:Property**, **rdf:XMLLiteral**, ...



## RDFS-Interpretations
_RDF-interpretations with a few extra constructs_

* Allows us to map **URI**s to **resources**, **untyped literals** or **class**


### Contains
_Everything in RDF-interpretations, plus..._

* $I_{CEXT}$: given a fixed RDF-representations, map resource to set of resources
	* $I_{CEXT}:IR\rightarrow 2^{IR}$
* 