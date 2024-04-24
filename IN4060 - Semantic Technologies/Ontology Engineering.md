_To create effective ontologies_

* It can be useful to use templates, like from [[OTTR (Reasonable Ontology Templates)|OTTR]] to simplify the complexity with abstractions
## Three main problems
1. Understanding the target domain
2. Identifying relevant abstractions over the domain e.g. "A panda is a mammal that eats only bamboo"
3. Formulating abstractions in a formal language like description logics

## Requirements
* If used for integration and communication, it should be generic, stable over time and precise

## Challenges

### Understanding the domain
* What to model
* Communication between ontology experts and domain experts

### How to model it
* Every mammal is either  male or female
	* As classes, properties, ...
* Depends on how it will be used

### Maintenance
* Fixing error
* Update ontology to support new use-cases
* Keeping ontology readable
	* navigation
	* Correct modularization

# Best practices
---
_Best practices of modeling ontologies in frameworks like OWL_

## Vocabularies

* Class names start with capital letter (PascalCase): *NamedPizza*
* Property names start with lower case (CamelCase): *hasTopping*
* Individuals start with capital letters (sometimes, lower case): *Diavolo*
* Singular names, not plural. *Diavolo* is a pizza, not a pizzas/pizze

## Classes vs. Individuals

* Sometimes difficult to distinguish between class/individual
* Can be both, depends on model
	* e.g. *Cat* can be either a class or a species
* **Rule of thumb**: What are data items, what are facts? That is probably your instances. Categorizations of data are classes
* [[OWL - loose ends#Punning|OWL Punning]] allows **OWL** classes, properties and instances to have the same IRI, but not under the hood

## Type vs. Subclass vs. Part

* *Stavanger is a City*: her *city* is the type, not a type. If it was a subtype, *Stavanger* would have to be a class itself
* **Classes** are collections of things, they have instances, they are not instances
* *Engine - Car*: Here *engine* is a part and not a subclass, because *engine* is not a type of *car*

## Problematic subclassing

* Is a *Student* a subclass of *Person*?
	* Can be problematic if a *Person* stops being a *Student*
	* Would be better as a **Role**
* **OntoClean** is a methodology for subsumptions
	* Rigidity
	* Identity
	* Unity
	* Dependegit nce

## Ontology Levels
_Ontologies are placed on different levels of abstraction_

* **Upper/top-level** ontologies: Physical ting, Process
* **Domain/mid-level** ontologies: Car, Pump, Cooling
* **Use-case ontologies**: Toyota Yaris, Ford SMax
* Ontology on the level above specifies one world vies or modeling methodology. Can help to structure ontologies on lower levels
* Is not always necessary, but can be useful

## Other good practices

* [[Main syllabus#OWL|OWL]] does not support exceptions
* Don't over-engineer
* Build for reuse and for a long life
* Don't be unnecessarily specific
* **KISS**: Keep it simple, stupid



# Requirement for building large scale ontologies
---

* Support large number of classes, which might have similar shapes
* Support a large number of industry standards
* Support consistent modeling
	* Semantically similar
	* Model the same thing in the same way, across different standards
* Support collaborative development
	* Contributors with varying background and competence
	* Model consistently between all contributors
* Support (automated) mechanisms for QA and verification

## Challenges of modeling consistently
* Humans are bad at repetitive tasks, especially in collaboration
* Often **Excel** is used, but it is not a good database tool as it allows duplicates and multiple different formats/structures
* Template libraries #toLink
