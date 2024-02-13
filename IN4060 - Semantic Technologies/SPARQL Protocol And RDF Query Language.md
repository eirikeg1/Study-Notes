_Query language for RDF defined by **W3C**_


* Semantic web equivalent of SQL, meant for [[RDF Overview|RDF]]
* [[Jena - Java library for RDF#Models|Jena Models]] can process **SPARQL**
* **SPARQL** keywords are case-insensitive


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


## Optional Patterns
_Allows a match to leave some variables unbound (NULL data)_

* A partial function from variables to RDF terms
* Groups may include optional parts
* `?x`and `?date` bound in every match, `?abs` bound if there is a Norwegian abstract
* Groups can contain several optional parts, evaluated separately

![[Pasted image 20240213172923.png|300]]

## Negation as Fa


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