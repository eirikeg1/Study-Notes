_RDF library for java_

* [Youtube tutorial](https://www.youtube.com/watch?v=nUdHneViLp4)

# Representations
---

*  Most basic [[RDF Overview|RDF]] representations covered by classes in `org.apache.jena.rdf.model`
* **IRI**s: Are represented with the standard `String` class in java
	* Some methods interpret `QNames` (geo:germany) but most don't
	* Can be useful to out namespaces in separate strings


## Models
_Represents a set of triples_

* Is an interface as well
* [[RDF Overview#Triples|Triples]] are stored in memory, for larger sets use some kind of _model database_ #toLink
* Object can be created by using `org.apache.jena.rdf.model.ModelFactory`
	```Java
	Model model = ModelFactory.createDefaultModel();
	```

* Models has the functions: 
	* `createResource(uri)` 
	* `createLiteral(uri)`
	* `createStatement(subject, predicate, object)` 
* Has the methods: 
	* `add(statement)`

## Resources 

* Resources are represented by the `Resource` interface
	* Has method `String getURI()`
* `org.apache.jena.rdf.model.Model` represents a set of RDF triples
* In Jena, Resources and Statements are linked to the Models they are part of
* `Model` objects also have the responsibility for creating `Resource`
* A resource can return its model with the method `getModel()` with `createResource(uri)`
* We can use the `.addProperty(property, object)` to add statements directly to the model

## Properties
_Subclass of Resource_

* Does not add anything to `Resource`, but can not be a blank node or a literal
* Can be created with the `Model` classes `createProperty(uri)` method

## Literals

* To create a literal with default type:
  ```Java
  Literal b = model.createLiteral("Berlin");
  ```

 * To create a literal with language tag:
   ```Java
   Literal d = model.createLiteral("Germany", "en")
   ```

* Alternative for Literals is from `org.apache.jena.datatypes.xsd.XSSDDatatype`
	```Java
	RDFDatatype type = XSDDatatype.XSDbyte;
	Literal n = model.createTypedLiteral("42", type);
	```

## Statements
_Also known as triples_

* To create a `Statement` you need:
	* A subject, which is a `Resource`
	* A predicate, which is a `Property`
	* An object, which is a `Resource` or `Literal`
* To create a statement use:
```Java
Resource berlin = model.createResource(geoNS + "berlin");
Property name = model.createProperty(geoNS + "name");
Literal b = createLiteral("Berlin");

Statement statement = model.createStatement(berlin, name, b);
```
* To add statement to model use the `add(statement)` method in `Statement`


## Other classes
_As Jena is a framework, there are differing implementations of data storage and processing_

* There are the classes `Triple` and `Graph`, which should not be mixed with `Statement` and `Model`
	* They are used for the Low level interface (for the Service Provider interface)
	* They are more simple and meant to be used for tasks such as creating your own database


# Using models
---

## Retrieving information

```Java
// Printing all with iterator
Iterator<Statement> it = berlin.listProperties();

while (it.hasNext()) {
	System.out.println(it.next()),
}

// Retrieve all with specific predicate with a `Property` object
Iterator<Statement> it = berlin.listProperties(property);

// can also be done through a object, without iteration
berlin.getProperty(property);


// Statements can be retrieved with
Iterator<Statement> sit = model.listStatements();


// To get all resources with a statement for a given predicate
Iterator<Statement> rit = model.listResourcesWithProperty(name);
```


## Pattern Matching

* To get all statements that have:
	* A given subject and object,
	* A given object,
	* A given predicate and **subject**,
	* Or any other combination
	
```Java
Iterator<Statement> sit = model.listStatements(subj, pred, obj);
```
* Where `subj`, `pred`, `obj` can be `null`to match any value ("wildcard")

## Read and write from/to file

* Models can read directly from files with `read()` and write with `write()`
```Java
Model m = ModelFactory.createDefaultModel();
m.read(new FileInputStream("Filename.ttl"), "", TTL);
m.write(new FileWriter("output.ttl"), "TTL");
```


### Writing to different formats

* The `FileManager`class allows you to write out the file in different formats

```Java
import org.apache.jena.util.FileManager

Model m = FileManager.get().loadModel(inputFile);
m.write(new FileWriter(("inputFile.ttl"), "", "TTL")) // Write to .ttl
m.write(new FileWriter(("inputFile.xml"), "", "RDF/XML")) // Write to XML
```

## SPARQL

* The most powerful way of retrieving data from a Model is through [[SPARQL 1.0 Protocol And RDF Query Language|SPARQL]]
*  Main  classes imported from `org.apache.jena.query`

### Main classes

```Java
QueryFactory // Creating queries in various ways
QueryExecution // Execution state of a query
QueryExecutionFactory // Create query executions (to get QueryExecution instances)
DatasetFactory // Create dataset instances

// For SELECT queries:
QuerySolution // A single solution to the query
ResultSet // All the QuerySolutions (an iterator)
ResultSetFormatter // Turn a ResultSet into various forms: text, RDF graph (Model, in Jena terminology or plain XML)

```


### Constructing and executing a query

```Java
String qStr =
	  "Prefix foaf: <" + fofNS + ">"
	+ "SELECT ?a ?b WHERE {"
	+ "  ?a foaf:knows ?b ."
	+ "} ORDER BY ?a ?b";

Query q = QueryFactory.create(qStr);

// To produce a QueryExecution for a given Query and Model:
QueryExecution qe = QueryExecutionFactory.create(q, model);
```

### Query execution

*  A query can be used several times, on multiple models
* `ResultSet` is a sub-interface of `Iterator<QuerySolution>`
* `QuerySolution` has methods to get a list of variables, value of single variables, etc.
* `QueryExecution` contains methods to execute different kinds of queries (**SELECT**, **CONSTRUCT**, ...)
* **N.B:** Important to call `close()` on query executions when no longer needed
```Java
// SELECT query:
ResultSet res = qe.execSelect();

// CONSTRUCT query:
Model constructModel = qe.execConstruct();

// Query a model:
Model model = ModelFactory.createDefaultModel();
model.read("http://heim.ifi.uio.no/martingi/foaf");
QueryExecutionFactory.create(q, model);

// Querying a Dataset:
String dftGraphURI = "http://heim.ifi.uio.martingi/foaf";
List namedGraphURIs = new ArrayList();
namedGraphURIs.add("http://richard.cyganiak.de/foaf.rdf");
namedGraphURIs.add("http://danbri.org/foaf.rdf");
Dataset dataset = DatasetFactory.create(dftGraphURI, namedGraphURIs);
QueryExecutionFactory.create(q, dataset);		   
```


### Conventions and security

* Antipattern: have user input in a query
* Tricky content of name can be a security issue
* Have to be careful to escape content of name properly
* Best to use [parameterized SPARQL strings](https://jena.apache.org/documentation/query/parameterized-sparql-strings.html)


## Example

![[Pasted image 20240213183122.png|400]]