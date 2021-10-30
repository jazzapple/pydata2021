# Knowledge Graphs in TerminusDB
Cheuk Ho

* TerminusDB is an open source knowledge graph data base
    * revision control features like Git - enabling collaboration with >1 developers
    * written in in Prologue and Rust
    * cloud hosted version on TerminusX (public beta): https://terminusdb.com/
* Demo: https://github.com/terminusdb/terminusdb-tutorials/tree/master/getting_started

## What is a semantic knowledge graph
* a data lake but with structure
* data comes out ... but can also go back in
* good at storing complex structures e.g. nested relationships
* uses **triples** to store data. This avoids complex joins and aggregations to get desired data
* supports revision control like Git operations
* flexible schema that user defines
* interactive viz in D3

## Components of a knowledge graph
* RDF: Resource Description Framework data model / semantic data model
* triple: smallest component of RDF.  a.k.a semantic triple, rdf triple
    * Set of 3 entities: **subject-predicate-object** e.g. Apple-is-red.
* quad
    * a triple with an extra element / dimension , e.g. fork of a repo, or a feature branch vs main branch
        * enables cross-referencing elements between the triples
        * allows us to create unique elements even with the same IDs
* Relational DB vs Graph Data model
    * Relational DB (SQL DB) consists of tables, columns , rows, keys. Order and structure is important. Needs joins and aggregations to retrieve info about relations of the data entities. csvs
    * Knowledge graphs consists of triples. Commonly storied in rdf/xml, ttl, JSON-LD. **Data is unstructured** - order does not matter as long as triples "paint same picture" they are the same data
        * easy to join without "trauma" e.g. traversing family tree c.f. flattening data into a data frame and doing multiple joins

**BUT WE STILL NEED SOME SORT OF SCHEMA!**
* build schemas in TerminusDB using **Document API**

### Schemas
* **objects** (a.k.a subdocuments). Collections of subdocuments are only meaningful when attached to a document, i.e. embedded. E.g. address has subdocuments street, number, suburb
* **documents**: single data entry in graph. Has its own ID. Documents are always top-level objects, never embedded insigde other objects. Using the Link Property, documents can be linked with each other. Default Document properties:
    * **name/id**: unique ID (like key)
    * **label/name**: numan readble name
    * **comment/description**: docstring for the object
* **enum**: symbolic name for **a set of values**  - e.g. values in a drop down list
* **properies**: can be data type (str, int, bool, decimal) properties or object properties 
    * has domain: class that is the subject of the property e.g. age
    * has range: type of data that the property belongs to e.g. integer
    * object properties are links between objects, e.g. employee (document) can have a manager, who is themselves a employee (document)

