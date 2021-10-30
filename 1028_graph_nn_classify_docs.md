# Classifying Documents using Graph Neural Networks
Slides: https://docs.google.com/presentation/d/104VMgVIkEsL0_DUS85q7yj3Rp-5VbWIHAsf97x6fsuk/edit#slide=id.p

## Garph ML Tasks
* Prediction levels:
    * node level: 
        * classifying academic paper categories - node=paper, edge=paper x cited by y        
    * community (subset of nodes/edges) level
    * edge-level
        * recommender systems (link predictions): nodes - users and items, edges: user-item interactions
        * access request: link prediction based on org structure and data access
    * graph level

## Message Passing
    * Label Proppagation = simplest form of message passing. Semi-supervised and iterative
        * nodes emit message about which label (state) they belong to, and accept messages from other nodes
        * nodes iteratively update state based on messages (e.g. majority vote)
    * More generally, Node info = hidden state
        * message can be a function of hidden state
        * different pooling methods c.f. majority vote to decide node state from neighbouring nodes

## How do Graph NNs work
* Universal framework for message passing on graphs
* Each message passing iteration is a layer in the NN
* Connected nodes in the graph are the neurons that connect to each other between layers

## Application of Graph NNs
* Classifying sensitivity of documents by types of users that access them

* Popular Graph NN packages: DGL, Python Geometric