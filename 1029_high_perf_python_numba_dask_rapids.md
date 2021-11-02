# HIGH PERFORMANCE PYTHON WITH NUMBA, DASK, AND RAPIDS FOR THE ABSOLUTE BEGINNER

* References: High Performance Python (O'Reilly): Micha Gorelick and Ian Ozsvold

## numba
* JIT compiler for Python code - 
* invoke via decorater `@numba.jit` around python function
```python
import numba

@numba.jit
def my_function:
    pass

# then call function as previous
```
* Uses cases: for loops, numpy arrays, broadcast functions

## RAPIDS
* https://rapids.ai/start.html
* Open source data science framework for GPU computation. API similar to pandas, numpy, scikit-learn
* installing RAPIDS also installs numba, Dask
    * pandas >> cudf
    ```python
    import cudf

    cudf.read_csv()
    # proceed as normal
    ```
    * numpy >> cupy
    * scikit-learn >> cuml
* but can still result in memory bottlenecks - data can't fit in memory - good use case for Dask

## Dask
* scale Python code across multiple cores
* supports data frames, arrays, custom
```python
# CPU cluster example
from dask.distributed import Client, fire_and_forget
import dask.dataframe as dd

client = Client()

ddf = dd.read_csv(...).persist()
ddf.groupby(...).attributename.mean().compute()
```

## Dask + RAPIDS
* circumvent memory bottleneck issues and still use GPU processing
```python
# GPU cluster example
import dask_cudf

drdf = dask_cudf.read_csv(....)
drdf.groupby(...).attributename.mean().compute()
```

### Dask + numba
* 
```python
# Uses Dask futures interface
from dask.distributed import Client, fire_and_forget
import numba

client = Client()

# Create numba JIT compiled function
@numba.jit
def my_function:
    pass

# Submit for computation by Dask client    
for i in range(500):
    img = client.submit(myfunc)
    future = client(submit(somefunc, img, 'filename.dat'))
    fire_and_forget(future)
```

### afar
* allows you to run GPU code from a single machine CPU
* beta version
```python
import afar
with afar.run, remotely:
    import dask_cudf
    ....
    res = (...)
res.result    
```