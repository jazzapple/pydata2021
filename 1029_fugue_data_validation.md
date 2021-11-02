# Large Scale Data Validation with Fugue

* `pip install fugue[all]`
* https://github.com/fugue-project/fugue

* Fugue Python package that provides an abstraction layer that enables porting of Pandas and SQL code to Spark and Dask processing
* Toggle between execution engines with `engine` parameter
* Allows Pandas code to be applied on Dask, Spark data frames directly in a distributed fashion


## Benefits of Fugue for data validation
* https://www.kaggle.com/goodwanghan/pydata-2021-scalable-data-validation-with-fugue
* Demonstrated using `Pandera`: lightweight data validation framework in Python
* Demo compares validation task using Pandera using Pandas, Dask and timings
* Fugue enables partitioning, such that validation functions can be simplified and applied to partitions - this delivers performance gains even just with Pandas dfs, and even more with Dask dfs
* `great_expectations` package demonstrates data validation witih `mostly` parameter, that allows some fixed proportion of observations to violate the assertion, and still pass. Designed to accomodate outliers in production

**Good candidate for scaling data validation tests**