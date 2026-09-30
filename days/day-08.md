# Day 8: Query with Spark SQL

## Goals
- Register a DataFrame as a temporary view and query it with SQL.
- Translate common SQL operations into DataFrame API calls and back.

## Learn
Read the [Spark SQL guide](https://spark.apache.org/docs/latest/sql-programming-guide.html) and [PySpark SQL quickstart](https://spark.apache.org/docs/latest/api/python/getting_started/quickstart.html#sql).

## Practice
1. Register a DataFrame as a temporary view.
2. Write a SQL query with filtering, grouping, aggregation, and ordering.
3. Recreate the same result using the DataFrame API.
4. Compare schemas and results to confirm equivalence.

## Deliverable
One SQL query and an equivalent DataFrame transformation, with a note about which form is clearer for your use case.

## Topic Notes
Register a DataFrame as a temporary view with `createOrReplaceTempView`; the view lives for the Spark session and does not copy the data into a separate table. Run SQL with `spark.sql`. SQL and the DataFrame API use Spark's Catalyst optimizer, so choose the form your team can review and maintain. Use explicit projections and aliases, and validate equivalent results by comparing values and schema.

```python
orders.createOrReplaceTempView("orders")
summary = spark.sql("""
	SELECT store_id, SUM(quantity * unit_price) AS sales_total
	FROM orders
	GROUP BY store_id
	ORDER BY store_id
""")
```

## Retail Example
Register the three order lines from Day 6. The query returns `East | 40.00` and `West | 40.00`. The SQL `GROUP BY` corresponds to DataFrame `groupBy("store_id").agg(...)`.

### Retail Questions and Answers
1. What does `createOrReplaceTempView` create? **A session-scoped SQL name for a DataFrame.**
2. What rows does the sample query return? **East with 40.00 and West with 40.00.**
3. Does using SQL instead of the DataFrame API bypass Spark's optimizer? **No; both are planned by Spark SQL.**

## Banking Assignment
Register synthetic transaction and account DataFrames as temporary views. Write SQL to calculate transaction count and total amount by branch and transaction type, then reproduce it with the DataFrame API. Compare schema and results, including how null branch values are handled.
