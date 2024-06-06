
* **The Resource Description Framework (RDF)** is a standard model for data  interchange
* Initially intended for annotation of web-accessible resources (1999)
* Later developed into a general purpose language for describing structured information, on the web or elsewhere
* Point of it is to have self-describing and self-documenting data
	* Decouples data from applications
	* Lightens the programming burden
	* Semantic Web applications should be/are generic and general purpose, exploiting rich and knowledge intensive data s
* ![[Pasted image 20240124122206.png|300]]

# Components 
---

## Triples

* All information is expressed using a **triple** pattern
* Triples can also be called a **statement**, or **fact**
* Triples consists of a **subject**, a **predicate** and an **object**
* The elements of and RDF triple are either URI references, literals, or blank nodes
![[Pasted image 20240124122447.png|300]]
* Literals and blank nodes may not appear everywhere in triples
* Because literals are just values, no relationships from literals allowed
* Blank nodes in predicate position deemed meaningless
![[Pasted image 20240124125209.png|300]]
* Triples are nice because they are flexible

## URIs
_Similar to URL, but more general_

* **Uniform Resource Identifiers**, are used to identify resources
* Usually strings in a special format, not necessarily referenceable (not a webpage or something, just a string)
* Should be unique, but is not strictly enforced
	* Two **URI**s are equal if and only if they are equivalent under Simple String Comparison, this includes ports
* **IRI**s (Internationalized Resource Identifier) are just URIs but encoded in Unicode.
* Naturally have a _global_ scope, unique throughout the web
	* Not checked for, but should be unique
* Examples of URIs:![[Pasted image 20240124122901.png|300]]
* Examples which are not URLs: ![[Pasted image 20240124123246.png|300]]

## QNames
_Shorter, more readable name to reference a URI_

* URIs are often long and hard to read and write.
* Most serializations use an abbreviation mechanism, like **prefixes** or **namespaces**
![[Pasted image 20240124123513.png|300]]
* This: 
	![[Pasted image 20240124123544.png|650]]
	turns to this:
	![[Pasted image 20240124123639.png|650]]
## Literals
_Used to represent data values_

* Have a datatype
* Datatypes are also resources, referenced via URIs, and written as:
	![[Pasted image 20240124123812.png|450]]
* Default value is string (in [[OTTR (Reasonable Ontology Templates)|OTTR]] and other places it is separate as strings does not have an **IRI**, think of it like a wrapper)
* Can specify the language of string with a language tag
	![[Pasted image 20240124124037.png|450]]
## Blank nodes
* Resources without an URI
* Can still map to other literals
* Blank nodes can not be references:
	  ![[Pasted image 20240124125344.png|400]]
* ![[Pasted image 20240124124931.png|400]]
# RDF Graphs
---

* An RDF graph is a set of triples
![[Pasted image 20240124124218.png|400]]
![[Pasted image 20240124124258.png|400]]
	
* Not all knowledge can be nicely represented with only triples with URIs and literals
* E.g. if we don't know the capital name, but the capital population:
![[Pasted image 20240124124706.png|400]]
* Some values are not good to structue in one string
![[Pasted image 20240124124808.png|400]]
* Can split up into multiple literals, but removes the convenience of an addresses

### Combining graphs

* Can be combined with union, but be beware of collisions
![[Pasted image 20240124140101.png|650]]
![[Pasted image 20240124140114.png|650]]
* You should usually rename locally named blank nodes
![[Pasted image 20240124140303.png|650]]

# Storage
---

* [[RDF Serializations|Multiple different serializations/formats]]
* Can be stored in files
	* Small RDF graphs
* From **SPARQL** endpoints
	* Data kept in a triple store (database)
	* served from endpoint as results of **SPARQL** queries
* **RDFizers** convert data to **RDF**
	* Tabular files (CSV, Excel): XLWrap
	* Relations DB: D2RQ or R2RML
	* W3C keeps a list


# Creating RDF data and vocabularies
---

* Designing an easy to use and robust namespace is non-trial
	* Naming is difficult
* Reuse existing vocabularies if possible, don't reinvent
* URIs are also addresses, consider publishing issues when naming
* Adhere to the policies described in best practice documents:
	* [Best Practice Recipes for Publishing RDF Vocabularies](http://www.w3.org/TR/2008/NOTE-swbp-vocab-pub-20080828/) 
	* [Cool URIs for the Semantic Web](http://www.w3.org/TR/cooluris)
* Use http://www.example.[com|net|org] for prototyping and documentation.

# Linked Open Data
---

## Tim berner-Lees recipe for 5 star web data

* Make data available on the Web (any format) under an open license. 
* Make it available as structured data (e.g., Excel, not image scans). 
* Use non-proprietary formats (e.g., CSV instead of Excel). 
* Use URIs to identify data items; make them referable on the Web. 
* Link your data to other’s data to provide context.