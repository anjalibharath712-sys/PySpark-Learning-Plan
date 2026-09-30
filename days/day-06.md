# Day 6: Summarize Data

## Goals
- Group records and calculate useful aggregates.
- Choose suitable aggregation expressions for a question.

## Learn
Review [grouping and aggregation](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/grouping.html) and the [functions reference](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/functions.html).

## Practice
1. Calculate record counts and totals by a category.
2. Calculate average, minimum, maximum, and distinct counts where meaningful.
3. Use conditional aggregation to count records that meet a rule.
4. Sort by a metric and limit the result to the top groups.

## Deliverable
A summary DataFrame answering three business-style questions about your sample data.

## Topic Notes
`groupBy` forms groups by one or more keys; `agg` computes one or more aggregate expressions per group. Common functions include `count`, `sum`, `avg`, `min`, `max`, and `countDistinct`. A grouped result has one row per group, and the key columns become output columns. Use aliases for clear output names. Grouping is generally a shuffle boundary, so aggregate only the columns needed and inspect plans for large workloads.

```python
summary = orders.groupBy("store_id").agg(
	F.sum(F.col("quantity") * F.col("unit_price")).alias("sales_total"),
	F.countDistinct("order_id").alias("order_count"),
)
```

## Retail Example
Use three order lines: East store has `R101` at 2 x 15.00 and `R102` at 1 x 10.00; West has `R103` at 4 x 10.00. Aggregate line sales by store. East totals 40.00 from two orders; West totals 40.00 from one order.

### Retail Questions and Answers
1. What is total sales across the sample? **80.00.**
2. What are the East and West totals? **40.00 each.**
3. What is the order count for West? **1.**

## Banking Assignment
Aggregate synthetic ledger entries by `branch_id` and `transaction_type`. Return transaction count, total amount, average amount, and distinct account count. State whether the amount is gross flow or signed net balance change, use clear aliases, and explain which result is appropriate for each question.
