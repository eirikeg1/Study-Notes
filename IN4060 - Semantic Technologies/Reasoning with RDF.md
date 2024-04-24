
# Inference Rules
---
#toExpand
* A **Calculus** is usually formulated:
	* set of axioms
	* set of inference rules
* **General inference rules** is premises $p_x$ and conclusion $P$
	* $\frac{P_{q},...,P_{n}}{P}$
* Inference rules may have
	* Any number of premises, but only one conclusion
	* $\models$ is entailment, $\models$ is inference #toExpand 
* Semantics and calculus are typical made to work in pairs, so one proves that:
	1. Every conclusion $P$ derivable in the calculus from a set of premises, is true in all interpretations that satisfy premises
	2. an conversely that every statement $P$ entailed by premises-interpretations is derivable in the calculus when the elements of premises are used as premises
	* Sound wrt the semantics, if 1 holds
	* Complete wrt the semantics if 2. holds
* By natural deduction you can derive multiple formulas from the top formula:
	* ![[Pasted image 20240221124441.png|300]]


## Model-Theoretic semantics
* #toExpand 


## Syntactic reasoning
* Syntactic methods operate only on the form of a statement on its *concrete grammatical structure*
* #toExpand 


# Inference for RDF
---

## RDF basics for inference

* Inference can be done in [[RDF Overview|RDF]]
* Can be thought of like a set of **Resources**, but is not actually
	* ![[Pasted image 20240221125447.png|300]]
* Inference is based on adding new triples to [[RDF Overview#RDF Graphs|RDF graph]], based on existing triples
* **RDFS** vocabulary allows classes and statements about classes
	* `rdfs:Resource`: class of all resources(resource)
	* `rdfs:type`: class of resources to classes they are members of (property)
* ![[Pasted image 20240221125326.png|400]]
* 


## Entailment with blank nodes
* Can be done if it has not been seem or used in the graph, or if it has been used for the same URI/literal/blank node
* \_:x represents B in se1 and A in se2
* ![[Pasted image 20240221125620 1.png|300]]

* ![[Pasted image 20240221125806.png|300]]


# RDF Reasoning patterns
---
* Type propagation
	* 2cv is car, all cars are vehicles, so...
* Property inheritance
	* 
* Domain and range reasoning



## Type propagation

* to combinations of `ref:typ`, `rdfs:subClassOf` and `rdfs:Class`
* Trigger recursive inheritance in a class taxonomy

### Rules
* Members of subclasses
	* ![[Pasted image 20240221132042.png|300]]
* Reflexivity of sub-class relation
	* ![[Pasted image 20240221132058.png|300]]
* Transitivity of sub-class relation
	* ![[Pasted image 20240221132113.png]]

### Example
![[Pasted image 20240221132140.png|400]]

## Property transfer

* Reasoning with properties depends on certain combination of `rdfs:subPropertyOf`, `rdf:type` and `rdf:Property`
* If and `rdfs:Class` is like a set of resources, then `rdf:Property` is like a relation on resources (not actually, but intuition)
* ![[Pasted image 20240221132546.png|400]]
### Rules
![[Pasted image 20240221132439.png|400]]

### Examples

![[Pasted image 20240221134131.png|400]]


#  Domain and range reasoning
_Typing data based on their use_

* Triggered by combinations of
	* `rdfs:range`
	* `rdfs:domain`
	* `rdf:type`
* Domain and range tell us how a property is used
* domain types the possible subjects of triples
* range types possible objects
* When we assert that property $p$ has domain $\text{\#C}$, we are saying
	* whatever is linked to anything by $p$
	* must be an object of type $C$
* 
![[Pasted image 20240221134914.png|400]]
![[Pasted image 20240221135200.png|350]]


## Rules
![[Pasted image 20240221134659.png|400]]
![[Pasted image 20240221134949.png|400]]


## Examples
* ![[Pasted image 20240221135053.png|350]]



## RDF axiomatic triples (excerpt)
* Some triples are axioms, can always be added to knowledge base
* ![[Pasted image 20240221135500.png|250]]
* From `:confucotr redfs:range :Person` we can derive:
	* ![[Pasted image 20240221135640.png|250]]


# Writing proofs
---

* Write one triple per line
* enumerate the lines
* write the rule name along with the line numbers corresponding to the assumptions
* Introduce triples from the knowledge base with the rule name $P$


## Example

* ![[Pasted image 20240221135939.png|350]]





# Chaining
---
_The process of setting new conclusions/rules based on  what you already know_

* Is done when evaluating a query, should you use the statements in the query, or are most facts already conputed? #Maybe

![[Pasted image 20240228122954.png|350]]
## Forward chaining

* Reasoning from premises to conclusions
* Add facts from conclusions of rules
* Entailed facts are stored and reused
* Precomputing and storing answers is suitable for data which is:
	* Frequently accessed, expensive to compute, relatively static
	* small enough to store efficiently

### Pros
* Optimizes retrieval
* No additional inference is necessary at query time

### Cons
* Increases storage
* increases overhead of insertion
* removal is problematic
* truth maintenance usually not implemented in RDF stores
* Problematic for distributed systems

## Backward chaining 

* Reasoning from conclusion to premises
* _What is needed for a conclusion to hold?_

### Pros
* Only relevant inferences are drawn
* Truth maintenance is automatic
* no persistent storage space needed

### Cons
* Not efficient when there is little need for reuse of computed answer
* Trades insertion overhead for access overhead (putting into database vs querying)
* Without caching, answer must be recomputed every time
### Example
![[Pasted image 20240228123446.png|350]]


# Reasoning in Jena
---
#toExpand
* Multiple ways in [[Jena - Java library for RDF|Jena]]
* Standard reasoner from `ReasonerRegistry.getRDFSReasoner();`
* ![[Pasted image 20240228124015.png|400]]
* 