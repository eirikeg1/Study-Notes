
# Syllabus
---

## RDF
_Standard model for data interchange_
* decouples data from applications
* Built up by triples

## SPARQL

### Exam 2023
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
