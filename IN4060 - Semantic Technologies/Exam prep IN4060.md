
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
HAVING (COUNT(?categoryCount) >= 3)

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
]

ex:Description[
	?id,
	?name,
	?description
]

ex:Property[
	?id,
	?name,
	?description,
	?domain,
	?range,
	?super_properties
] :: {
	ex:DomainRange(?id, ?domain, ?range),
	ex:Description(?id, ?name, ?description),
	ottr:Triple()
} .

```

