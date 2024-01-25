
# Different types of serializations
---

* **DRF/XML** is the original W3C standard, complicated:
![[Pasted image 20240124131859.png|500]]
* **Turtle** is convenient as well as human readable/writeable:
![[Pasted image 20240124131934.png|500]]
* **N-triples** had one triple per line, without allowing abbreviations:
![[Pasted image 20240124132043.png|500]]
* Other formats include N3, TriX, TriG, RDF/JSON, ...


# Turtle
---

* Allows any non-zero amount of space in between elements in triples
## URI references and triples

![[Pasted image 20240124132243.png| 750]]


## Namespaces

* QNames (namespaces) are written without special characters 
![[Pasted image 20240124132442.png|750]]

## Literals

![[Pasted image 20240124132705.png|500]]


## Statements sharing elements

* Use semicolons instead of period to use same [[RDF Overview#Triples|subject]]

![[Pasted image 20240124132742.png|750]]
![[Pasted image 20240124132759.png|700]]
![[Pasted image 20240124132949.png|700]]
![[Pasted image 20240124133019.png|700]]
![[Pasted image 20240124133031.png|700]]

## Blank nodes

* Are represented with underscores, or square brackets
* If using underscore, should have a local identifier represented as `:identifier`
	* Identifiers are only used when reading to a file, not after parsing

![[Pasted image 20240124133100.png|700]]


## Other things

* [Turtle specifications](http://www.w3.org/TR/turtle/)

![[Pasted image 20240124133832.png|700]]