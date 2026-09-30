# Day 7: Combine DataFrames

## Goals
- Join DataFrames on explicit keys and understand join types.
- Prevent accidental row multiplication and ambiguous columns.

## Learn
Review [DataFrame joins](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.DataFrame.join.html) and the [Spark SQL guide](https://spark.apache.org/docs/latest/sql-programming-guide.html).

## Practice
1. Create a fact DataFrame and a small lookup DataFrame.
2. Compare inner, left, and semi joins; explain which records each retains.
3. Check key uniqueness before joining and compare row counts before and after.
4. Rename or select overlapping fields to make the output schema unambiguous.

## Deliverable
A joined DataFrame with a documented join type, key, and row-count check.

## Topic Notes
Join on explicit key expressions and choose the join type based on which unmatched records matter. An inner join retains matches; a left join retains every left row; a semi join returns left rows that have a match without adding right-side columns; an anti join returns left rows without a match. Check that the dimension-side key is unique before joining, because duplicate keys multiply fact rows. Rename or qualify overlapping columns before selecting the result. Join hints such as broadcast should be evidence-based, not automatic.

## Retail Example
Order lines are `(O1, A, 2)`, `(O2, B, 1)`, `(O3, X, 4)` for `(order_id, sku, quantity)`. A product lookup maps `A -> Produce` and `B -> Bakery`; `X` is not listed. A left join retains all three order lines and gives `X` a null department. An inner join retains only `O1` and `O2`.

### Retail Questions and Answers
1. How many rows result from the left join? **3**, assuming product SKUs are unique.
2. How many rows result from the inner join? **2.**
3. What does a null department for SKU `X` signal? **There was no matching product row; it should be investigated or handled by an explicit unknown-product policy.**

## Banking Assignment
Join synthetic transactions to an account reference table on `account_id`. Compare left and inner joins, preserve transactions with missing account metadata, and check that the reference key is unique before joining. Report unmatched transaction count and explain why dropping unmatched financial events can harm reconciliation.
