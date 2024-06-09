
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

## Question 2 Properties

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


## Question 3 New region and wine

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


## Question 4 Wines and region

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

## Question 5 French single grape wine

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


## Question 6 Makers

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


## Question 7 Red wine from Sancerre

```SPARQL
ASK WHERE {
	?wine a :Wine;
		:hasColor :Red;
		:locatedIn :SancerreRegion .
}
```


## Question 8 Grapes used in Bordeaux but not in Loire

```SPARQL
SELECT ?wine
WHERE

```