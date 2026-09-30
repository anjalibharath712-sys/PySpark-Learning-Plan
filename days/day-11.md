# Day 11: Learn RDD Fundamentals

## Goals
- Explain what an RDD is and how it relates to DataFrames.
- Recognize when a lower-level RDD operation is justified.

## Learn
Read the [RDD programming guide](https://spark.apache.org/docs/latest/rdd-programming-guide.html), focusing on transformations, actions, and persistence.

## Practice
1. Create an RDD from a small collection and apply `map`, `filter`, and `reduce`.
2. Express an equivalent operation with a DataFrame.
3. Compare the schema and optimization information available in each approach.
4. Use an RDD only for a task that benefits from its lower-level interface.

## Deliverable
A short comparison and a reasoned choice of API for new structured-data work.

## Topic Notes
An RDD is Spark's lower-level distributed collection abstraction. Its transformations (`map`, `filter`, `flatMap`) are lazy; actions (`count`, `collect`, `reduce`) execute work. RDDs offer flexible object-level processing but do not carry a relational schema for Catalyst to optimize. For structured data, DataFrames usually provide clearer schemas and query optimization. RDDs remain useful for some unstructured or specialized low-level tasks; avoid converting DataFrames to RDDs without a concrete need.

```python
sku_rdd = spark.sparkContext.parallelize(["A", "B", "A"])
counts = sku_rdd.map(lambda sku: (sku, 1)).reduceByKey(lambda left, right: left + right)
```

The equivalent structured operation is typically a DataFrame `groupBy("sku").count()`.

## Retail Example
Given SKU observations `A, B, A`, the RDD word-count pattern produces `(A, 2)` and `(B, 1)`. A DataFrame with a `sku` column can calculate the same counts while retaining its schema and using relational optimizations.

### Retail Questions and Answers
1. What are the two SKU counts? **A: 2; B: 1.**
2. Is `map` an action? **No; it is a lazy transformation.**
3. Which API is the usual first choice for tabular sales data? **DataFrames, because they preserve schema and enable SQL optimizations.**

## Banking Assignment
Use synthetic transaction types to count events with an RDD transformation/action, then implement the same result with a DataFrame `groupBy`. Compare readability, schema availability, and query planning. Explain why transaction tables should normally stay in the DataFrame API.
