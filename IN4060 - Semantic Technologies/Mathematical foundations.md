
# Basic set theory
---

![[Pasted image 20240214125053.png|350]]
## Set
_Unordered collection of elements without duplicates_

* Notation for set with 1, 2 and 3: $\{1, 2, 3\}$
* Notation for $a$ is in set $B$: $a\in B$
	* $1\notin \{\}$
*  Often used to define properties
	* 3 is a natural number: $3\in \mathbb{N}$
* **Empty set** $\emptyset$ or $\Set{}$
* $a$ is **subset** of $b$ if every element in $a$ is also in $b$, but $b$ has more elements
	* $a\subset b$
	* **Subset or equal**: $\subseteq$
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


# Propositional logic
---

## Different kinds of logic
_Formalizes different aspects of reasoning, defined mathematically_

* **Propositional logic**: AND, OR, NOT
* **Description logic**: A mother is a person who is a female and has a child
	* Most relevant to [[Course Page - IN4060|IN4060]]
* **Modal logic**: Alice knows that Bob didn't know yesterday
* **First-order logic**: For all ..., for some ...

### Propositional logic

* **Formulas** are defined **by induction** or **recursively**
* Any letter $p,q,r,\dots$ is a formula
* If $A$ and $B$ are formulas, then
	* $A\land B$ is also a formula
	* $A\rightarrow B$ is a formula
	* $\neg A$ is a formula
* Many formulas can be simplified to **atomic form**
* If $a\land b$ then both $a$ and $b$ must also be true
* Can be parsed uniquely, as every symbol has unique binding strength:
![[Pasted image 20240214134037.png|400]]

#### Terminology #toExpand 

* $\neg, \land, \lor, \rightarrow$ are **connectives**
* A formula $(A\land B)$ is a **conjunction**
* A formula $(A\lor B)$ is a **disjunction**
* A formula $(A\rightarrow B)$ is an **implication**
* A formula $\neg A$ is a **negation**
* Formulas can be equivalent: $(a\land a)\Leftrightarrow a$
* **Atomic formulas** can not be simplified, **compound formulas** can
	* Compound formula $I$ where $I={a,b}$, then $I\rightarrow (a\land b)$
* A formula which always is true $(a\lor \neg a)$ is a **tautology**
* A set of only true elements is an **interpretation** #Maybe
* **Entailment**: if $A$ then $B$ $(A\models B)$
* $if$, $iff$ (if and only if)

#### Interpretations
* Set of true statements
* Can either be True or False (satisfied) in an _environment_, or world
* Interpretation $I$ satisfies set $A$ if all elements in $I$ is true in $A$
	* $I\models A$
* ![[Pasted image 20240214135253.png|300]]

#### Entailment / Tautologies
* If an Interpretation $I$ means a formula $a$ has to be true, you can say $I$ **entails** $a$ $(I\models a)$
* Formula $A$ is called a **Tautology** if $A$ is True in all possible interpretations
* Can be shown by simply: $\models A$
	* $\models (a\lor \neg a)$
* 