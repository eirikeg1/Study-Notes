
# Basic set theory
---

## Set
_Unordered collection of elements without duplicates_

* Notation for set with 1, 2 and 3: $\{1, 2, 3\}$
* Notation for $a$ is in set $B$: $a\in B$
*  Often used to define properties
	* 3 is a natural number: $3\in \mathbb{N}$
* **Empty set** $\emptyset$ or $\{\}$
* $a$ is **subset** of $b$ if every element in $a$ is also in $b$, but $b$ has more elements
	* $a\subset b$
	* **Superset** $\supset$ is the opposite
* **Union** $\cup$ is an operation which returns the set which is all the elements in two other sets
* **Intersection** $\cap$ is an operation which returns the elements two sets have in common
* **Set difference** of a and b $a\setminus b$ is an operation which returns the elements which is in $a$ but not $b$
* **Symmetric difference** $\Delta$ is operation which gets the elements in $a$ and $b$ but not in both
* A **Relation** $R$ between two sets $A$ and $B$ is a set of pairs $\langle a, b\rangle\in A\times B$
	* Can have operations on relations
	* $R$ is a **subrelation** $P$ if $R\subset P$

### Set comprehensions
* Sometimes enumerating all elements is not good enough
* Used to make general statements
* Alle elements in $A$ has given property$\{x\in A|x$ has some property$\}$

### Cross product

* Set of all pairs $\langle a,b \rangle$ with $a\in A$ and $b \in B$
* Notated $A\times B$

## Pair
_Ordered collection of two objects_

* Notated by: $\langle 1, 2\rangle$

## Relations

### Properties
* **Reflexive**: $xRx$ for all $x\in A$
	* e.g. $=$
* **Symmetric**: if $aRb$, then $bRa$
* **Transitive**: if $aRb$ and $bRc$, then $aRc$

### Number of relations
* If $A=\{1,2\}$, there are 16 relations on $A$
	* $\emptyset\in A, \{1\}\in A,\dots$
* All possible relations on $A$ is $2^{|A|^2}$
* Can use **operations** on relations, as they are actually sets
	* Father set $F$ and Mother set $M$ and parent set $P$
	* $F\cup M=P$



# Examples
---

![[Pasted image 20240214125053.png|500]]