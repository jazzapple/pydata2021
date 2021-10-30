# Computations as Assets - a New Approach to Reproducibility and Transparency
`pip install accelerator`
https://expertmakeraccelerator.org/installation/ (OS requirements: Ubuntu, Debian, FreeBSD)
https://github.com/exaxorg
https://github.com/eBay/accelerator

* Open source project, `Exax`: Python library for parallel processing and streaming of large datasets. 
* Computations are stored on disck and easily retrieved and re-used when needed
* Been around since 2012. Open sourced by eBay

## Problem
* Intermediate datasets are created and passed between programs, i.e. 
```python
# prog1.py
df = (...)

with open('tempfile.pickle', 'wb') as outfile:
    pickle.dump(df)

# prog2.py
with open('tempfile.pickle', 'rb') as infile:
    df = pickle.load(infile)
```
<insert jpeg>
* how to know what source code created a given data object? 

## Benefits
1. minimise risk for manual mistakes
    * reproducible workflow that can be taken to production
    * output always corresponds to current source code
2. maximise efficiency
    * re-use, don't re-compute
    * parallel processing
* **Intermediate data files are fetched by function, i.e. deterministic based on source code!!**


# What it does
* uses build scripts, which cross reference data provenance    
* takes care of management of intermediate dataset, or "bookkeeping"

# How it works
* stores data as a data set
* columnar storage
* read, processa adn write all slices in parallel
* solving data locality problem - partition dataset using hash function
* Designed to run on single machine 
* but not compatible with parquet, clusters

<insert jpeg
