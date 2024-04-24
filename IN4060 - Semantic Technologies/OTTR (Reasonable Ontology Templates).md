* Ongoing research and innovation project at IfI
* Used to make [[Ontology Engineering]] easier
* Macro/Pattern language or knowledge bases
* Abstractions over RDF and OWL
* Goal is to improve the efficiency and quality of ontology engineering for large scale ontologies
* **DRY** principle: Do not Repeat Yourself
* [Otter website](www.ottr.xyz)

## Template-driven methodology
* You need **manual input**, as well as generated dumps
* We want to allow the domain expert to be able to describe table structures into a format which can be made into an **OTTR template**

#### Pipeline
$\dfrac{\text{Tabular format}}{\text{domain expert}}\rightarrow\dfrac{\text{user}}{\text{data manager}}\rightarrow\cdots$ #toExpand 


# Abstractions
---
* Uses **modeling patterns** (similar to API calls)
* OTTR allows you to make templates of commonly used patterns 
* Multiple pizzas have the same properties/subclasses/types, but different values. Why not make a 'function-type' to just take in the values and use the same properties/subclasses/types

## Example
#toExpand 


# Templates
---
_Way to abstract away complexity, similar to functions in programming_
* Compositional patterns
* Encapsulates complexity
* Ensure completeness of input
* Separate design and content
*  Macro expansion
* **Template signature**, name and parameters

## Base template
_Template without definition_
* Every other template needs to implement this template.
* Can have many different base templates
* For example $\text{ottr:Triple[?subject, ?predicate, ?object] :: BASE}$

## Types
* Written before, like in **Java**
* Similar to programming language types
* Can be put before parameter declarations to do type checking
* Ensures all instances can be correctly expanded to a proper RDF-graph 
* Helps highlight template's intention
* Supports lists

### Base-types
* Limited to classes and datatypes defined in XSD, RDF, RDFS and OWL

## Non-blank parameters
_Ensures the parameter is not a blank node_
* Notated with **!** before
* Can also force **IRI**s of entities

## Optional parameters
* Notated with **?**

## Default values 
* Assigned with **=** in signature

## Multiple values
* Parameters can be lists, but you usually want to make a connection from a to everything in b, not the list b itself
* Solved with expansion modes

## Expansion modes
### Cross product
* Starts with `cross |` and 'mark' the list with `++`
### Zip
* Combines the `i` elements in multiple lists
* Starts with `zipMin |` and 'mark' the lists with `++`


# Different Serializations
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



# Template libraries
---
_Set of design principles to standardize templates_

* Saved as **LOD** principles
* One example is [OTTRs template library](https://tpl.ottr.xyz/)
* Publish patterns as a **Pattern API**

## OTTR
### Top down modeling with different abstraction levels
* System-> domain -> logical -> utility -> base

## Removing redundancy

### Two types of redundancy
_Should be performed with some caution, not  always natural to change for them_
* **Lack of reuse**: Pattern captured by existing pattern
* **Uncaptured pattern**: Pattern not captured by template, create new template for pattern

## Lutra
_Open source Java CLI tool for OTTR templates_

* Automatically creates formatted data from different template libraries
* Can map data from **Excel sheets** or [[SPARQL 1.1|SPARQL]] queries
* Supports [[#Different Serializations]]
