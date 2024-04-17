* Ongoing research and innovation project at IfI
* Used to make [[Ontology Engineering]] easier
* Macro/Pattern language or knowledge bases
* Abstractions over RDF and OWL
* Goal is to improve the efficiency and quality of ontology engineering for large scale ontologies
* **DRY** principle: Do not Repeat Yourself
* [Otter website](www.ottr.xyz)

## Abstractions
* Uses **modeling patterns** (similar to API calls)
* OTTR allows you to make templates of commonly used patterns 
* Multiple pizzas have the same properties/subclasses/types, but different values. Why not make a 'function-type' to just take in the values and use the same properties/subclasses/types

## Example
#toExpand 


## Templates
_Way to abstract away complexity, similar to functions in programming_
* Compositional patterns
* Encapsulates complexity
* Ensure completeness of input
* Separate design and content
*  Macro expansion
* **Template signature**, name and parameters

### Base template
_Template without definition_
* Every other template needs to implement this template.
* Can have many different base templates
* For example $\text{ottr:Triple[?subject, ?predicate, ?object] :: BASE}$

### Types
* Written before, like in **Java**
* Similar to programming language types
* Can be put before parameter declarations to do type checking
* Ensures all instances can be correctly expanded to a proper RDF-graph 
* Helps highlight template's intention
* Supports lists

#### Base-types
* Limited to classes and datatypes defined in XSD, RDF, RDFS and OWL

### Non-blank parameters
_Ensures the parameter is not a blank node_
* Notated with **!** before
* Can also force **IRI**s of entities

### Optional parameters
* Notated with **?**

### Default values 
* Assigned with **=** in signature

### Multiple values
* Parameters can be lists, but you usually want to make a connection from a to everything in b, not the list b itself
* Solved with expansion modes

### Expansion modes
#### Cross product
* Starts with `cross |` and 'mark' the list with `++`
#### Zip
* Combines the `i` elements in multiple lists
* Starts with `zipMin |` and 'mark' the lists with `++`


# Serializations
---

## stOTTR
_Easier to read and write_
#toExpand 

## wOTTR
_OWL vocabulary for semantic web use_

## tabOTTR
_Tabular format for bulk template instances_

## bOTTR
_ETL mappings to **OTTR** instances_
* Allows running [[SPARQL 1.0 Protocol And RDF Query Language|SPARQL]] queries



