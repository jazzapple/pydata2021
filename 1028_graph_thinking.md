# Graph thinking
* Slides: https://derwen.ai/s/kcgh
* `kglab` package: https://derwen.ai/docs/kgl/

## Benefits of graphs
* Normalisation can obscure patterns in data for relational DBs, compared with network views
    * acknowledges complexity of context
    * identify emergent patterns e.g. finding similar nodes, finding customers of customers, **betweenness centrality** metric
* Can help reveal metadata and business rules, e.g. data integration problems    

## Context
* Framework by Dave Snowden - quadrant of
    * Complex: sense problems > graph analytics fits well
    * Complicated: assess facts
    * Chaos: identify stability
    * Simple: establish facts 
* Analysis tools can perform poorly in Chaos as more suited to Complcated/Simple

## Types of Graphs
* Property graphs
* SEmantic graphs (RDF)

* Graph neural networks - geometric deep learning
    * knowledge graph embeddings

## Graph theory
* Graphs can be converted into matrices - algebraic graph theory
* *Within graph data, dimensionality is an essential component of the trade of between symbolic and numeric representation*

## Tools
* **kglab** package - integration between graph libraries with heavily used data science packages
    * useful for NLP use cases
* parquet format efficient for serialisation of graph data
* **SHACL**: validation of RDF graphs, like unit tests