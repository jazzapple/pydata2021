# POLARS, THE FASTEST DATAFRAME LIBRARY YOU NEVER HEARD OF
* https://pola-rs.github.io/polars-book/user-guide/index.html
* https://github.com/pola-rs/polars

* Written in Rust: memory safe programming lanugage. Concurrency, memory utilisation control
* Apache Arrow as memory model

## Polars in a nutshell
* Fastest data frame libraries out there: https://h2oai.github.io/db-benchmark/
    * Runtime: 5-20 times faster than Pandas
    * Memory requirement: 5x less than Pandas
* columnar data storage
* other stuff I haven't heard of (predicate pushdown, copies are free)
* lazy evaluation and declarative (what we want) rather than procedural (how to do it), so leaves room for optimisation
* parallelised (multi-threaded)
* can be combined with numpy unfuncs
* supports custom functions via apply
* in-memory processing, so scales from 0GB to ~500GB as an estimate

## How to use it
* `Fn(Series) -> Series`
    * expr output is input for another expr, can be combined infinitely
    * reduces need for custom python functions
```python
import polars as pl

df = pl.DataFrame(
    {
        "A": [1, 2, 3, 4, 5],
        "fruits": ["banana", "banana", "apple", "apple", "banana"],
        "B": [5, 4, 3, 2, 1],
        "cars": ["beetle", "audi", "beetle", "beetle", "beetle"],
    }
)
# sum the column "foo"
df.select(pl.sum("foo"))

# group by bar and sum foo
df.groupby("bar").agg(pl.sum("foo"))
```    
* window functions: `col("foo").aggregation_expression(...).over("column to groupby")`
* where: `df.filter(col("cars") == "beetle")`
* selecting columns
```python
df.select([
    pl.all().exclude("cars")
    ])
```
* combine sequential and parallel functions
* chaining of methods
```python
(df
    .sort("fruits")
    .select([
    "fruits",
    "cars",
    lit("fruits").alias("literal_string_fruits"),
    col("B").filter(col("cars") == "beetle").sum(),
    col("A").filter(col("B") > 2).sum().over("cars").alias("sum_A_by_cars"),       # groups by "cars"
    col("A").sum().over("fruits").alias("sum_A_by_fruits"),                        # groups by "fruits"
    col("A").reverse().over("fruits").flatten().alias("rev_A_by_fruits"),          # groups by "fruits
    col("A").sort_by("B").over("fruits").flatten().alias("sort_A_by_B_by_fruits"),  # groups by "fruits"
    np.exp(col("A")).alias("exponent")
    ])
)
```
* fast I/O
* apply
```python
(df.select([
    "fruits",
    "cars",
    "A",
    col("A").apply(lambda x: np.exp(x)).alias("a_new")
]))
```