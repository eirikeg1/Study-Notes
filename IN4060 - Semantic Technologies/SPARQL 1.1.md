

* Builds on [[SPARQL 1.0 Protocol And RDF Query Language|SPARQL 1.0]]
* [Documentation](https://www.w3.org/TR/sparql11-query/)


# Query language
---

## Assignments and expressions

* Value of expression can be assigned/bound to variable
* can be used in **SELECT**, **BIND** or **GROUP** **BY** clauses

![[Pasted image 20240410122642.png|350]]
### BIND
_Keyword which assigns expressions to variables_
![[Pasted image 20240410122411.png|350]]


## Aggregates: Grouping and filtering
_Takes several results of query and collapses together_

* sum, count etc...
* Similar to SQL
* Solutions can be grouped
* Aggregates are applied per group

### HAVING
_Filters after aggregation_
* In contrary to **FILTER**
* In example below the **HAVING** happens last
* ![[Pasted image 20240410123139.png|350]]

### Aggregate functions

* ![[Pasted image 20240410123654.png|350]]


## Subqueries
_Embed SPARQL queries within other queries_

* Gives ability to compute intermediate values in a subquery
* Subqueries evaluated logically first, results bind variables in the outer query
* Only variables selected in subquery will be visible in the outer queries scope

![[Pasted image 20240410124147.png]]


## Negation in SPARQL 1.1

* Assumes [[Model Semantics & Reasoning#Closed World Assumption|Closed world assumption]] and unique names

### IN SPARQL 1.0
* Does not have negation for **Monotonicity**
	* Adding new triples never remove statements, only remove
* Can be worked around with **BOUND** keyword
	* ![[Pasted image 20240410124609.png|350]]
* Because loophole, why not just add it?

### MINUS
* A MINUS B evaluates bot A and B giving solutions $sol(A)$ and $sol(B)$, then checks intersection
* #toExpand
* ![[Pasted image 20240410124813.png|350]]


### FILTER NOT EXISTS
* Evaluates A for each solution
* Evaluates based on shared variables
![[Pasted image 20240410125043.png|350]]


### MINUS and FILTER NOT EXISTS differences
#toExpand
![[Pasted image 20240410125222.png|400]]


## Property paths
_Small property-oriented query language inside the language, used to simplify needlessly complex statements._

* Takes the place of the **predicate** of the graph pattern
* E.g. weire `foaf:maker|dct:ceateor` instead of UNION
* ![[Pasted image 20240410131750.png|350]]
* ![[Pasted image 20240410131802.png|400]]
* ![[Pasted image 20240410132140.png|350]]


# Federated Query

* **SPARQL 1.1**
### SERVICE 
_Keyword which instructs a federated query processor to invoke a portion of SPARQL query against a remote SPAEQL service/endpoint_

* SPARQL service is any implemetation conforming to SPARQL 1.1 Protocol for RDF
* ![[Pasted image 20240410132644.png|350]]

# UPDATE Language
---

* The difference between **UPDATE** and [[SPARQL 1.0 Protocol And RDF Query Language#CONSTRUCT|CONSTRUCT]] is that **CONSTRUCT** is an alternative for **SELECT**
	* Instead of returning an RDF graph according to template, **UPDATE** actually changes the data
* Keywords **INSERT** and **DETELE**
* ![[Pasted image 20240410132957.png|350]]
* Can also insert statements you don't already have
	* ![[Pasted image 20240410133115.png|350]]
* ![[Pasted image 20240410133143.png|350]]
* Can delete everything based on **WHERE**:
	* ![[Pasted image 20240410133241.png|350]]
* Often, you would delete triples, then add new, possibly in same or different graphs
	* ![[Pasted image 20240410133327.png|350]]
	* ![[Pasted image 20240410133340.png|350]]
* You can delete/insert from named graphs
	* ![[Pasted image 20240410133424.png|350]]
	* ![[Pasted image 20240410133453.png|350]]
## Whole graph operations
![[Pasted image 20240410133619.png|400]]


# Entailment Regimes
---

* Basic graph patters by means of subgraph matching: simple entailment
* Solutions that implicitly follow from the queried graph: entailment regimes
	* **RDF entailment**, **RDF Schema entailment**, **D-entailment**, **OWL 2 RDF-Based semantics entailment**, OWL2 direct semantics entailment, RIF simple entailment

## Complexities

![[Pasted image 20240410135734.png|400]]


## Example

![[Pasted image 20240410134407.png|400]]

![[Pasted image 20240410134417.png|400]]

New triples from different regimes:
![[Pasted image 20240410134730.png|400]]


## OWL 2 Direct Semantics Entailment Regime
#toExpand


## OWL 2 RDF-based Semantics Entailment Regime
#toExpand 



