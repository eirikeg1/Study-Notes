
# Task 1
---
## 1.1 DL Axioms
### Statements
3. $\text{Horse}\sqsubseteq \text{Animal}$
4. $\text{Animal}\sqsubseteq(\text{Male}\sqcup \text{Female})$
5. $(\text{Male}\sqcap \text{Female})\sqsubseteq\bot$
13. $\text{MonteHorse}\sqsubseteq (\text{RaceHorse}\sqcup\forall \text{hasCompeted.HorseRace})$
14. $\text{SuperHorse}\sqsubseteq{(\text{RaceHorse}\sqcap\text{hasWon}\geq_{100})}$
15. $\forall\text{hasWon.HorseRace}\sqsubseteq{\exists \text{hasCompeted.HorseRace}}$
19. $\text{RaceHorse}\sqsubseteq\forall\text{hasTrainer.Person}$
21. $\text{trains}\equiv \text{hasTrainer}^{-}$

### Individual-statements
1. $\set{\text{RexRodney}}\sqsubseteq{\text{SuperHorse }}\sqcap$
	$\forall\text{hasTrainer.Kjell\_Håkonsen }\sqcap$
	$\forall\text{hasWon.Elitloppet1986 }\sqcap$
	$\forall\text{hasSire.Doctor\_Rodney}$
2. $\set{\text{Elitloppet1986}}\sqsubseteq{(\text{HorseRace}\sqcap\neg\text{MonteRace})}$
3. $\set{\text{"Steady, Ready, Go"}}\sqsubseteq{\text{Filly}\sqcap\text{MonteHorse}}$

## 1.2
1. Unknown. It is not specified if Rex Rodney is a Male or Female
2. Yes, Kjell Håkonsen had interest in Elitloppet 1986 
3. Unknown. We don't have enough information to know this.
4. No. It is a filly, which means it is maximum 3 years old. It is also a Monte horse, and all warmblooded Monte horses must be at least 4 years old.
5. We know she is not warmblooded, but this does not necessarily make it coldblooded as of the stated rules
6. It did not. It is a Monté horse, while Elitloppet 1986 is not a monté-race

## 2.1
1. "In the Wings" and "Northern Dancer"
   ![[Pasted image 20240516093307.png]]
2. Doctor Rodney
   Native Dancer
   In the Wings
   Nearco
   Nearctic horse
   Shirley Heights
   ![[Pasted image 20240516093239.png]]
   
3. This is because Ancestor is not set as a transitive property

# Task 3
---
## 3.1
This is because both **OrderOfMammals** and **OrderOfAnimals** are both classes. In Description Logic a class cannot be the instance of another class. The Punning mechanism doesn't actually allow one class to be member of another class. Punning is dependent where something can be interpreted as either a class or individual, but never both at the same time.


## 3.2
OWL 2 can in some cases be hard for a human to understand, as it is highly logical and designed to effectively be interpreted by a reasoner. In order to make things clearer for people to understand OWL2 has included annotations. Annotations can be looked upon as some kind of 'documentation' or 'metadata'.

The five different types of annotations: (`owl:versionInfo`, `rdfs:label`, `rdfs:comment`, `rdfs:seeAlso` and `rdfs:isDefinedBy`) has their own purposes. The name of each property does explain very well what their purpose is. By using them it makes it easier for a human to understand what is going on. `seeAlso` can also be used to link to other sources, which can give a greater understanding of the ontology.


## 3.3
3. This is both a valid EL and QL axiom
4. This is not valid in either
5. This is also valid for both
13. This uses universal quantification to the right of "SubclassOf", which is allowed in EL, but not QL
14. This is valid in both
15. This uses universal quantification at the start, and is therefore not valid EL or QL
19. This is valid in both
21. This is valid EL, but since it uses SameIndividual it is not valid. It is not legal in QL though.