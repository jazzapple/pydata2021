# Deep Neural Deduplicatoion

* DNN + Contrastive Learning

## Problem
* Web construction themed article de-duplication
* Existing rule-based heuristics
* Data stewards manually identify duplicates
    * Large labelled datasets (millions)
* Records are dictionaries of named entities. Named entites extracted from free text
    * e.g. 
    ```json
    "project_title": "Renovation of empire state building",
    "project_address": "34th Street",
    "project_value_millions": 5 
    ```
    * mix of text and numeric attributes
* Supervised learning for duplicates not feasible due to expensive comparison of articles
* Distance between article embeddings >> contrastive learning

## Contrastive Learning
* Representation learning technique that learns an embedding space where similar records are located near each other and far away from dissimilar ones
* Facenet paper: **Triplet loss** - Anchor, Positive, Negative
    * find embeddings such that distance between Anchor and Positive match is more than the distance between Anchor and Negative match
    * in practice, executed in batches
    * finding the optimal set of triplets can be done either
        * Batch All: average the loss over hard and semi-hard triplets
        * Batch hard: for each anchor select the hardest positive and hardest negative
* Does not neccearily require labels, and can be applied in unsupervised setting        

## Solution
* Text features: SBERT (BERT with similarity) embeddings
* Numeric features: feed forward network
* Resulting in a Concategnate Embeddings vector for each article
* Challenge for computation:
    * many records
    * high dimensionality
* Compare embeddings in distance matrix (cosine similarity) - expensive comparison for exhaustive search
    * possibly utilise Approximate Nearest Neighbour Search to segment space and search for neighbours within it (reducing search space)
* Instead, used ElasticSearch metadata filtering to reduce search space - records published in a certain time range
