# Day 5: Clean Rows and Values

## Goals
- Filter rows with DataFrame expressions.
- Identify and handle null, duplicate, and invalid values deliberately.

## Learn
Review the [DataFrame API](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/dataframe.html) and [SQL null semantics](https://spark.apache.org/docs/latest/sql-ref-null-semantics.html).

## Practice
1. Filter records using multiple conditions with `&`, `|`, and parentheses.
2. Count nulls in important columns and inspect duplicate keys.
3. Choose and explain a policy for missing values: retain, replace, or filter.
4. Add a validation rule for impossible values, such as negative quantities.

## Deliverable
A cleaning function that returns a DataFrame and before/after quality counts.

## Topic Notes
Filter with `where` or `filter` and Spark column expressions. Combine conditions with `&` and `|`, enclosing each comparison in parentheses; Python `and`/`or` do not construct Spark expressions. Use `isNull`/`isNotNull` to test missingness because comparisons with SQL `NULL` evaluate to unknown. `dropDuplicates` removes duplicate rows or duplicate keys, but only do so after defining which record is authoritative. Data-quality policy should be explicit: count invalid rows, quarantine them, or reject a batch instead of silently dropping data.

```python
valid = orders.filter(
	F.col("quantity").isNotNull()
	& (F.col("quantity") > 0)
	& F.col("customer_id").isNotNull()
)
```

## Retail Example
Consider four input rows: `S1, C10, qty=2`; `S2, customer=NULL, qty=1`; `S3, C20, qty=-1`; and a repeated `S1, C10, qty=2`. Keep rows with a customer and positive quantity, then deduplicate by `sale_id`. Record counts at each stage so discarded or repeated sales are visible.

### Retail Questions and Answers
1. How many input rows have a null customer? **1.**
2. How many rows have a positive quantity before deduplication? **3.**
3. How many rows remain after requiring a non-null customer, positive quantity, and unique `sale_id`? **1 (`S1`).**

## Banking Assignment
Given synthetic transfers with a nullable `customer_id`, possible duplicate `transfer_id` values, and `amount`, define quality rules: required identifiers must be present, amounts must be positive, and transfer IDs must be unique. Write filters and duplicate checks, report counts before and after each rule, and explain how you would quarantine rejected transfers rather than lose audit evidence.
