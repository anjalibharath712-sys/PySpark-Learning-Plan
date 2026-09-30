# Day 4: Transform Data

## Goals
- Select, rename, derive, and remove columns using the DataFrame API.
- Build readable transformations with built-in functions.

## Learn
Review the [PySpark quickstart](https://spark.apache.org/docs/latest/api/python/getting_started/quickstart.html) and [SQL functions reference](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/functions.html).

## Practice
1. Select only the fields needed from your sample data.
2. Rename a column and create a derived column with `withColumn`.
3. Use `cast` to convert a string field into a numeric or date type.
4. Drop an unnecessary column and verify the result schema.

## Deliverable
A transformation that produces a clean, consistently named DataFrame without changing its source.

## Topic Notes
Use `select` to project columns, `alias` or `withColumnRenamed` to name them, and `withColumn` to derive or replace a column. These operations return a new DataFrame; they do not mutate the input. Build expressions with `pyspark.sql.functions` (`F`) and `pyspark.sql.Column` operations rather than Python loops over rows. Explicit casts help keep output types stable.

```python
from pyspark.sql import functions as F

sales = orders.withColumn(
	"line_total", F.col("quantity") * F.col("unit_price")
).select("order_id", "quantity", "unit_price", "line_total")
```

## Retail Example
For order `R101`, `quantity = 2` and `unit_price = 15.00`, so `line_total = 30.00`. Derive the line total with a Spark column expression, then select only the fields needed downstream. This transformation remains distributed until an action runs.

### Retail Questions and Answers
1. What is the line total for `R101`? **30.00.**
2. Does `withColumn` modify the original `orders` object? **No; it returns a new DataFrame.**
3. Why prefer `F.col("quantity") * F.col("unit_price")` to a Python row loop? **Spark can plan and execute the expression across partitions.**

## Banking Assignment
Transform synthetic ledger rows by renaming `txn_id` to `transaction_id`, selecting only transaction and account fields, and creating `signed_amount`: credits are positive and debits are negative. Keep the original DataFrame unchanged, and document the chosen sign convention. Use decimal-compatible expressions for amounts.
