
# Syllabus
---

## RDF
_Standard model for data interchange_
* decouples data from applications
* Built up by triples

## SPARQL


# Exam 2023
---
#### Question 7
```SPARQL
SELECT ?game ?year
WHERE {
	?game a bg:Game .
	?game bg:category bg:abstractStrategy .
	OPTIONAL {?game bg:releaseYear ?year .}
}
```

#### Question 8
```SPARQL
SELECT ?game (COUNT(?category) AS ?categoryCount)
WHERE {
	?game a bg:Game .
	?game bg:Category ?category .
	?category a bg:Category .
}
GROUP BY ?game
HAVING (COUNT(?category) >= 3)
```

#### Question 9
```SPARQL

```


# Exam 2022
---

## SPARQL
### Question 2 Properties

```OTTR
ex:DomainRange[
	ottr:IRI ?id,
	ottr:IRI ?domain,
	ottr:IRI ?range
] :: {
	ottr:Triple(?id, rdfs:range, ?range),
	ottr:Triple(?id, rdfs:domain, ?domain)
} .

ex:Description[
	ottr:IRI ?id,
	xsd:string ?name,
	xsd:string ?description
] :: {
	ottr:Triple(?id, foaf:name, ?name),
	ottr:Triple(?id, dc:description, ?description)
} .

ex:Property[
	ottr:IRI ?id,
	xsd:string ?name,
	xsd:string ?description,
	ottr:IRI ?domain,
	ottr:IRI ?range,
	List<ottr:IRI> ?super_properties
] :: {
	ottr:Triple(?id, rdf:type, rdf:Property),
	ex:DomainRange(?id, ?domain, ?range),
	ex:Description(?id, ?name, ?description),
	cross | ottr:Triple(?id, rdfs:subPropertyOf, ++?super_properties)
} .
```


### Question 3 New region and wine

```SPARQL
INSERT DATA {
	GRAPH <http://www.w3.org/TR/2003/PR-owl-guide-20031209/wine#> {
		:BourgueilRegion a :Region;
			:locatedIn :LoireRegion .
		:bretonBourguielTrinch2019 a :Wine;
			:madeFromGrape :CabernetFrancGrape;
			:hasMaker :Breton;
			:hasColor :Red;
			:locatedIn :BourgeilRegion;
			:year 2019;
			:hasFlavour :Middle .
	}
}
```


### Question 4 Wines and region

```SPARQL
SELECT ?wine ?region ?label
WHERE {
	?wine a :Wine;
		:hasColor :Red;
		:locatedIn ?region .
	OPTIONAL {
		?wine rdfs:label ?label .
	}
}
```

### Question 5 French single grape wine

```SPARQL
SELECT ?wine
WHERE {
	?wine a :Wine ;
		:madeFromGrape ?grape;
		:locatedIn ?region .
	FILTER (?wine = :LoireRegion || ?wine = :BourdeauxRegion)
}
GROUP BY ?wine
HAVING (COUNT(?grape) = 1)
```


### Question 6 Makers

```SPARQL
CONSTRUCT {
	?wineMaker rdfs:SubClassOf :WineMaker;
		:makesWine ?wine;
		:locatedIn ?region .
}
WHERE {
	?wine a :Wine;
		:hasMaker ?wineMaker;
		:locatedIn ?region .
}
```


### Question 7 Red wine from Sancerre

```SPARQL
ASK WHERE {
	?wine a :Wine;
		:hasColor :Red;
		:locatedIn :SancerreRegion .
}
```


### Question 8 Grapes used in Bordeaux but not in Loire

```SPARQL
SELECT DISTINCT ?grape
WHERE {

	{
		?region a :Region.
		OPTIONAL {?region :locatedIn ?location}
		FILTER {?region = :BordeauxRegion || ?location = :BordeauxRegion}
	}
	?wine a :Wine;
		:madeFromGrape ?grape;
		:locatedIn ?region.
	FILTER NOT EXISTS {
		?wine :locatedIn :LoireRegion
	}
	FILTER {?region = :BordeauxRegion || ?region = :StEmilionRegion}
}
```


### Question 9 Old Bordeaux wines

```SPARQL
SELECT ?wine
WHERE {
	{
		SELECT ?loireYear
		WHERE {
			?oldest a :Wine;
				:locatedIn+ :LoireRegion;
				:year ?loireYear .
		}
		ORDER BY ASC ?loireYear
		LIMIT 1
	}
	?wine a :Wine;
		:locatedIn+ :BourdeauxRegion;
		:year ?year.
	FILTER (?year < ?loireYear)
}
```


## Section 4: Description Logic and OWL

### Question 20 John
```Manchester Syntax
(SubClassOf Men and some hasChild)(john)
```

### Question 21 BiologicalParents



### Question 22 Person
```D
(Boat or Car) not SubSetOf Person
```
$\text{Boat}\sqcup \text{Car}\sqsubseteq{\neg\text{Person}}$

### Question 23 Childless
$\text{Childless}\sqsubseteq{(\exists{hasChild}.\text{Person}\sqsubseteq\bot)}$


## SHACL

### Question 28 SHACL

```SHACL
:ResidentInNorwayShape a sh:NodeShape;
	sh:targetClass ex:ResidentInNorway ;
	sh:property [
		sh:path ex:NorwegianID;
		sh:minCount 1;
		sh:maxCount 1;
		sh:datatype xsd:string;
		sh:minLength 11;
		sh:maxLength 11;
		sh:pattern "^[0-9]"
	] ;
	sh:property [
		sh:path ex:liveIn;
		sh:hasValue ex:Norway
	] .
	

```



# Exam 2019
---
## SPARQL

### 2a Accounts and Account holders

```SPARQL
SELECT ?number ?holder 
WHERE {
	?account a bank:Account;
		bank:accountAtBank bank:DLB;
		bank:accountHolder [foaf:name ?holder];
		bank:accountNumber ?number .
}
```


### 2b Conflicting balances

```SPARQL
SELECT ?account DISTINCT ?dateTime 
WHERE {
	?account a bank:Account;
		bank:date ?dateTime;
		bank:hasBalance [
			bank:amount ?amount
		] .
}
ORDER BY ?dateTime
```


### 2c Account statement

```SPARQL
SELECT ?when ?in ?out
WHERE {
	?transaction a bank:Account;
		bank:date ?when .
	
	OPTIONAL {
		?transaction bank:toAccount dlb:10001;
			bank:amount ?in .
	}
	OPTIONAL {
		?transaction bank:fromAccount dlb:10001;
			bank:amount ?out
	}
}
```



### 2d Accounts with high inflow

```SPARQL
SELECT ?accountNumber SUM(?amount)
WHERE {
	{
		?account a bank:Account;
			bank:accountNumber ?accountNumber .
	}
	?transaction a bank:Transation;
		bank:toAccount ?account;
		bank:amount ?amount;
		bank:date ?date;
		
	FILTER(year(?date) = 2010)
	
}
GROUP BY ?account
HAVING (SUM(?amount) > 100000)
```












