

# 1 Model Semantics
---
## 1.1 Exercise: Interpretation
### $\mathcal{I}_{1}\models \Gamma_{1}$

* $\Delta^{\mathcal{I^{1}}}=\set{1,2,3,b1}$
* $\Lambda^{\mathcal{I^{1}}}=\set{Alonso, JJ}$
* $\beta^{\mathcal{I^{1}}}=\set{b1}$
* $\Lambda^{\mathcal{I^{1}}}=\text{All strings in graph } \Gamma^{\mathcal{I^{1}}}$

* $\text{:Tweety}^{\mathcal{I^{1}}}=1$
* $\text{:JollyJumper}^{\mathcal{I^{1}}}=2$
* $\text{:Bruce}^{\mathcal{I^{1}}}=3$

* $\text{:Penguin}^{\mathcal{I^{1}}}=\set{1}$
* $\text{:Fish}^{\mathcal{I^{1}}}=\set{3}$
* $\text{:Horse}=\set{2, 3}$
* $\text{:Vegetable}^\mathcal{I^{1}}=\set{}$

* $\text{:Bird}^{\mathcal{I^{1}}}=\set{1}$
* $\text{:Animal}^\mathcal{I^{1}}=\set{1,2,3}$
* $\text{:Food}^\mathcal{I^{1}}=\set{3,\text{b1}}$

* $\text{:eats}^\mathcal{I^{1}}=\set{\langle{1,3}\rangle, \langle{2,b1}\rangle}$
* $\text{:likes}^\mathcal{I^{1}}=\set{\langle{2,1}\rangle}$
* $\text{:hasNickname}^\mathcal{I^{1}}=\set{\langle{2,JJ}\rangle,\langle{3,Alonso \rangle}}$
* $\text{:favoriteFood}^\mathcal{I^{1}}=\set{\langle{1,3}\rangle, \langle{2,b1}\rangle}$

### $\mathcal{I}_{2}\nvDash \Gamma_{1}$

* $\Delta^{\mathcal{I_{2}}}=\set{1, b1}$
* $\beta^{\mathcal{I}}(\text{\_:b})=b1$
* $\text{:Tweety}^{\mathcal{I}_{2}}=\text{:JollyJumper}^{\mathcal{I}_{2}}=\text{:Bruce}^{\mathcal{I}_{2}}=1$
* $\text{:Food}^{\mathcal{I_{2}}}=\set{1}$
* $\text{:likes}^{\mathcal{I_{2}}}=\set{\langle{1,1}\rangle}$
* $\text{:Animal}^{\mathcal{I_{2}}}=\set{\emptyset}$


## 1.2 Exercise: Entailment

1. :Tweety is an animal
	1. $\text{:Tweety rdf:type :Penguin}$
	2. $\text{:Penguin rdfs:subClassOf } \text{:Bird}$
	3. $\Gamma\models\text{:Tweety rdf:type :Bird}, 1, 2, \text{rdfs9}$
	4. $\text{:Bird rdfs:subClassOf :Animal}$
	5.  $\Gamma\models\text{:Tweety rdf:type :Animal | } 3, 4, \text{rdfs9}$
2. :Tweety likes :JollyJumper
	1.  Counter model $C^{1}=\mathcal{I_{1}}$
	2.  $\text{:Tweety}^{C^{1}}=1$
	3. $\text{:likes}^{C^{1}}=\set{\langle2,1\rangle}$
	4. Because $1$ is not the object in any of the elements in $\text{:likes}$, the relation $:likes$ does not contain $\langle \text{:Tweety, :JollyJumper}\rangle$
3. :Food is the range of :favoriteFood
	1. Food is in the range of :favoriteFood, but one can not make a derivation of this using the RDF and RDFS entailment rules. It is however entailed as $\Gamma$ includes the triple $\text{:eats rdfs:range :Food}$
4. :Bruce has some favorite food
	1.  Counter model $C^{2}=\mathcal{I_{1}}$
	2. $\text{:favoriteFood}^{C^{2}}=\set{\langle{1,3}\rangle, \langle{2,b1}\rangle}$
	3. $\text{:Bruce=3}$
	4. Because the relation $\text{:favoriteFood}^{C^{2}}$ does not contain a tuple $\langle3,x \rangle$ for any $x$, this is not entailed.
5. :Bruce is a vegetable
	1. Counter mode $C^{3}=\mathcal{I_{1}}$
	2. $\text{:Vegetable}^\mathcal{C^{3}}=\emptyset$
	3. Because it is explicitly stated that $\text{:Vegetable}^\mathcal{C^{3}}=\emptyset$, $\text{:Bruce}$ can not be a vegetable
6. :Bruce is a horse
	1. $\text{:Bruce :hasNickname }Alonso$
	2. $\text{:hasNickname rdfs:domain :Horse}$
	3. $\Gamma\models \text{:Bruce rdf:type :Horse | }1,2,rdfs2$
7. :Bruce is a fish
	1. $\text{:Bruce rdf:type :Fish}$
	2. This does not need to be proven with entailment rules, as it is explicitly stated in triple 1.



# 2. Semantic web and reasoning
---

1. the **Closed World Assumption** is an assumption that if a thing is not listed in the knowledge base, it does not exist. The **Open World Assumption** states that there might be things not mentioned in the knowledge base. In practice if something is not stated or derivable the **Closed World Assumption** will consider it false, while the **Open World Assumption** will consider it true. The **Open World Assumption** is better for the semantic web, as you realistically can't take every fact on the internet, across domains, into consideration.

2. The **Unique Name Assumption** assumes that all entities with the same identifier must be the same entity. The **Non-Unique Name Assumption** assumes that different entities can share identifiers. In the semantic web the **Non-Unique Name Assumption** is the most applicable one. This is because the semantic web  is a decentralized network with different representations for each database. Because two different databases can model things differently, they may actually represent two different entities with the same identifier.

3. In essence the difference between **forward chaining** and **backward chaining** is that in **forward chaining** you reason from premises to conclusions, while in **backward chaining** you reason from already established conclusions to new premises. **Forward chaining** is used when to add facts from conclusions of rules, while **backward chaining** is used to find out what is needed for a conclusion to hold.
   
   Forward chaining is useful when you want to derive all possible conclusions from a given set of facts. Backwards chaining is better suited for problem solving tasks where you have a specific goal in mind and need to determine what information is required to achieve that goal.
   
   Forward can incrementally update knowledge base as new facts are added, and when new facts are added they can quickly be incorporated and be used to derive 
   new facts.
   
   Backwards chaning,  being goal drive, needs to explore the whole inference chain to reach a conclusion. Therefore the addition of new facts may require re-evaluating the entire reasoning process to determine if the new information affects the conclusion.

4. **Soundness** means that is a conclusion can be derived with the RDFS entailment rules, then the conclusion is a logical consequence of the RDFS semantics. Therefore the entailment rules never produce any invalid inferences.

5. **Completeness** means that any entailment can be found using the rules. The RDFS rules are not complete, because there exists valid inferences according to the RDFS semantics that cannot be derived using the rules alone.

# 3 RDF(S) formal semantics
---

## 3.1 Exercise

The main difference between the semantics for RDF from **Foundations of Semantic Web Technology** and the lectures is mainly the representations. In the lectures we represent the semantics by first-order logic and set theory. **FSWT** represents it's semantics using functions. The lectures also use a the **Unique Name Assumption**, **FSTW** does not. **FSWT** allows us to map URIs to resources, untyped literals or classes.

While the lectures have more concrete representations of types of resources, the model theoretic semantics represents them more abstractly into IR, IP and IC.


## 3.2 Exercise

$IR=\set{tw,jj,ty,sc,sp,Pr,do,ra,re,li,cl,An,Pen}$
$IP=\set{li,ty,do,sc,sp,ra,cl}$
$\mathcal{IC}=\set{An,Pen,Pr,cl,re}$

$I_{S}(\text{:Tweety})=tw$
$I_{S}(\text{:JollyJumper})=jj$

$I_{S}(\text{:likes})=li$
$I_{S}(\text{rdf:type})=ty$
$I_{S}(\text{rdfs:domain})=d$o
$I_{S}(\text{rdfs:subClassOf})=sc$
$I_{S}(rdfs:subProperty)=sp$
$I_{S}(\text{rdfs:range})=ra$
$I_{S}(\text{rdf:Class})=cl$
$I_{S}(\text{rdf:Resource})=re$

$I_{S}(\text{:Animal})=An$
$I_{S}(\text{:Penguin})=Pen$
$I_{S}(\text{rdf:Property})=Pr$


$I_{EXT}\,\,=\;li\rightarrow\set{\langle b,tw\rangle}$


$I_{EXT}\,\,=\;li\rightarrow\set{\langle b,tw\rangle}$
	    $ty\rightarrow\{\langle{An,cl}\rangle,\langle{Pen,cl}\rangle,\langle{tw,Pen}\rangle,\langle{tw,An}\rangle,\langle{sp,re}\rangle,\langle{sp,Pr}\rangle$
		    $\;\;\,\,\langle{li,Pr}\rangle,\langle{ty,Pr}\rangle,\langle{do,Pr}\rangle,\langle{sc,Pr}\rangle,\langle{ra,Pr}\rangle,\langle{cl,Pr}\rangle,\langle{re,re}\rangle,$
		    $\;\;\,\,\langle{jj,re}\rangle,\langle{ty,re}\rangle,\langle{sc,re}\rangle,\langle{Pr,re}\rangle,\langle{do,re}\rangle,\langle{ro,re}\rangle,\langle{An,re}\rangle,$
		    $\;\;\,\,\langle{Pen,re}\rangle,\langle{tw,re}\rangle,\langle{sp,re}\rangle,\langle{do,re}\rangle,\langle{ra,re}\rangle$$\langle{cl,cl}\rangle,\langle{Pr,cl}\rangle,\langle{re,cl}\rangle\}$
		    
	    $do\rightarrow\set{\langle{li,An}\rangle}$
	    $ra\rightarrow\set{\langle{li,An}\rangle}$
	    $sc\rightarrow\{\langle{An,re}\rangle,\langle{Pen,re}\rangle,\langle{Pr,re}\rangle,\langle{An,An}\rangle,\langle{Pen,Pen}\rangle,\langle{Pr,Pr}\rangle,$
			$\;\;\;\langle{re,re}\rangle\langle{Pen,An}\rangle\}$
		$sp\rightarrow\set{\langle{li,li}\rangle,\langle{ty,ty}\rangle,\langle{do,do}\rangle,\langle{sc,sc}\rangle,\langle{ra,ra}\rangle,\langle{cl,cl}\rangle}$

$\mathcal{I}_{CEXT}=An\rightarrow\set{b,tw}$
		$Pen\rightarrow\set{tw}$
		$Pr\rightarrow\set{li,ty,do,sc,sp,ra,cl}$
		$re\rightarrow\set{jj,tw,t,sc,sp,Pr,do,ra}$
		$cl\rightarrow\set{An,Pen,Pr,re,cl}$


## 3.3 Exercise

$I_{S}=\text{:OrderOfAnimals}\rightarrow oA$
	$\:\text{:OrderOfMammals}\rightarrow oM$
	$\:\text{:OrderOfBirds}\rightarrow oB$
	$\:\text{:Eagle}\rightarrow ea$
	$\:\text{:Elephant}\rightarrow el$
	$\:\text{:Bobo}\rightarrow bo$
	$\:\text{:Joe}\rightarrow bo$
	$\:\text{rdf:type}\rightarrow ty$
	$\text{:rdfs:subClassOf}\rightarrow sc$
	$\text{Pr}\rightarrow pr$
	$\text{rdf:Resource}\rightarrow re$
	$\text{rdf:Class}\rightarrow cl$

$IR=\set{oA,oM,oB,ea,el,bo,ty,sc,re,pr,cl}$
$IP=\set{sc,ty}$
$IC=\set{oA,oB,oM,re,cl}$

$I_{EXT}=\;\;sc\rightarrow\{\langle{oB,oB}\rangle,\langle{oB,re}\rangle,\langle{oB,oA}\rangle,\langle{oM,oA}\rangle,\langle{oM,re}\rangle,\langle{oM,oM}\rangle\}$
			$\:\;\;\langle{oA,oA}\rangle,\langle{oA,re}\rangle, \langle{re,re}\rangle,\langle{cl,cl}\rangle,\langle{cl,re}\rangle\}$
		$ty\rightarrow\{\langle{oM,oA}\rangle,\langle{oM,cl}\rangle,\langle{oB,oA}\rangle\,\langle{oA,pr}\rangle,\langle{oA,cl}\rangle,\langle{oA,pr}\rangle,\langle{oM,cl}\rangle,$
			$\,\,\;\;\langle{ea,oB}\rangle,\langle{ea,Oa}\rangle,\langle{ea,ea}\rangle,\langle{el,el}\rangle,\langle{el,aM}\rangle,\langle{el,eA}\rangle,\langle{bo,el}\rangle,$
			$\,\,\;\;\langle{bo,ea}\rangle,\langle{bo,bo}\rangle,\langle{ty,pr}\rangle,\langle{ty,re}\rangle,\langle{ty,ty}\rangle,\langle{sc,pr}\rangle,\langle{sc,sc}\rangle,\langle{pr,pr}\rangle,$
			$\,\,\;\;\langle{re,re}\rangle,\langle{pr,re}\rangle,\langle{cl,cl}\rangle,\langle{cl,re}\rangle,\langle{oM,re}\rangle,\langle{oA,re}\rangle,\langle{oB,re}\rangle$
			$\,\,\;\;\langle{oB,cl}\rangle \langle{re,cl}\rangle\}$

$I_{CEXT}=\,oA\rightarrow\set{oA,re}$
		$oB\rightarrow\set{re,oA,oB}$
		$oM\rightarrow\set{re,oM,oA}$
		$re\rightarrow\set{re}$
		$cl\rightarrow\set{oA,oB,oM,re,cl}$







