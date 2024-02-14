_Query language for RDF defined by **W3C**_


* [Jena SPARQL documentation](http://jena.apache.org/documentation/javadoc/arq/)
* Semantic web equivalent of SQL, meant for [[RDF Overview|RDF]]
* [[Jena - Java library for RDF#Models|Jena Models]] can process **SPARQL**
* **SPARQL** keywords are case-insensitive
* Many sites (wikidata, dbpedia, dbtunes) publish **SPARQL** endpoints
	* **SPARQL** queries can be submitted to a database server that sends back the results
* Protocol is http, defined by **W3C Web Services** as defined [here](http://www.w3.org/TR/rdf-sparql-protocol/)


# Type of Queries
---

## SELECT
_Compute table of bindings for variables_

![[Pasted image 20240213165639.png|300]]

## CONSTRUCT
_Use bindings to construct a new RDF graph_

* Uses similar syntax to [[RDF Serializations#Turtle|turtle]]
![[Pasted image 20240213165724.png|300]]


## ASK
_Returns boolean value based on query_

![[Pasted image 20240213165938.png|300]]


## DESCRIBE
_Returns an RDF graph with data about matching resources_

* Usually returns triples containing something somewhere in the triple
* Not often used, as can be unpredictable

![[Pasted image 20240213170026.png|300]]


# Solution sequence and modifiers
---

## Sequence modifiers
_Applied in this order_
* **Order**
* **Projection**: Remove some columns
* **Distinct**: Eliminates duplicates
* **Reduced**: Allows to remove some or all duplicate solutions
	![[Pasted image 20240213170736.png|400]]
* **Offset**: Do not return the $x$ first results
	* Not meaningful without **ORDER BY**
* **Limit**: Only return the $x$ first results


# Graph Patterns
---
* A **Basic Graph Pattern** is a set of triple
* Uses same syntax as in [[RDF Serializations#Turtle|turtle]]
* Scope of blank node labels is the **Basic Graph Pattern**
![[Pasted image 20240213171303.png|400]]

## Grouping

* Several Graph Patterns can be used with `{}`
* The scope of a **FILTER** constraint is the group where the filter appears
* Group containing one basic graph pattern:
	* ![[Pasted image 20240213171637.png|300]]
* Two groups with one basic graph pattern each:
	* ![[Pasted image 20240213171702.png|300]]

### Groups with constraints or filters
_Groups can contain constraints or filters_

![[Pasted image 20240213171847.png|400]]


## Optional patterns
_Allows a match to leave some variables unbound (NULL data)_

* A partial function from variables to RDF terms
* Groups may include optional parts
* `?x`and `?date` bound in every match, `?abs` bound if there is a Norwegian abstract
* Groups can contain several optional parts, evaluated separately

![[Pasted image 20240213172923.png|300]]

## Negation as failure
_Even though there is no negation operator, there is a workaround_

* Testing if a graph pattern is not expressed, but specifying an **OPTIONAL** graph pattern that introduces a variable, and then testing if it is not bound
	![[Pasted image 20240213173327.png|300]]

## Matching alternatives (UNION)
_Matches if any of some alternatives matches_

* In example below the book will only be retrieved if either the author or the book matches
* Shorthand with `|`:
![[Pasted image 20240214154847.png|350]]
![[Pasted image 20240213173519.png|300]]


## Graph graph pattern (RDF datasets)
_You can do queries over multiple datasets_

* SPARQL queries are executed against a **RDF dataset**
* A **RDF dataset** contains
	* One **default graph** (unnamed graph)
	* Zero or more **named graphs** identified by an URI
* **FROM** and **FROM NAMED** keywords allows to select an RDF dataset by reference
	* The **default graph** will consist of the RDF merge of the graphs referred to in the **FROM** clauses
	* **FROM NAMED** clauses will define the different named graphs
	* Note that, if there is no FROM clause, but there are **FROM NAMED** clauses, the default graph will be empty

![[Pasted image 20240213174151.png|350]]
![[Pasted image 20240213174309.png|350]]


# Keywords
---

* **PREFIX**: Used to set prefixes
* **?**: Indicates the following text is a variable, like for example a column header. In example below the identifier is placed into the `?jd`
* **SELECT**: Same as **SQL**, gets data
* **DISTINCT**: Only get one occurrence of following keyword/variable
* **Blank nodes**: Same syntax as in [[RDF Serializations#Blank nodes|turtle]], with either `_:identifier` or `[]`(can contain triples)
* **FILTER**: Is followed by a boolean expression
* **STR**: Convert to string
* **ORDER BY**: Sorts results based on following expression
	* **ASC**
	* **DESC**

## Functions and operators

* **Binary operators**: $||, \&\&, =,!=,<,>,<=,>=,+,-,*,/$
* **Unary operators**: $!, +, -$
* **Unary tests**: bound(?var), isURI(?var), isLiteral(?var)
* **Accessors**: str(?var), lang(?var), datatype(?var)
* Regex is used to match a variable with a regular expression. Always use with str(?var)
	* e.g.: `regex(str(?name), "Os")`


# Examples
---

![[Pasted image 20240213115436.png|400]]
![[Pasted image 20240213162636.png|400]]

![[Pasted image 20240213115902.png|400]]
![[Pasted image 20240213162839.png|400]]

![[Pasted image 20240213162925.png|400]]
![[Pasted image 20240213163008.png|300]]

![[Pasted image 20240213163203.png|400]]
![[Pasted image 20240213163224.png|300]]


![[Pasted image 20240213164320.png|400]]

![[Pasted image 20240213181518.png|400]]