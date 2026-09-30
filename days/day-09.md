# Day 9: Use Built-in Functions

## Goals
- Transform strings and dates with Spark SQL functions.
- Work with nested data without prematurely converting rows to Python objects.

## Learn
Browse the [PySpark functions reference](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/functions.html) and [Spark SQL data types](https://spark.apache.org/docs/latest/sql-ref-datatypes.html).

## Practice
1. Normalize text with trimming, case conversion, and a regular-expression replacement.
2. Parse a date string, derive year and month, and calculate a date difference.
3. Create a DataFrame with an array or struct and select a nested field.
4. Handle malformed input explicitly and inspect output types.

## Deliverable
A reusable transformation that cleans a string field and derives at least two date-based columns.

## Topic Notes
Built-in functions in `pyspark.sql.functions` create expressions Spark can optimize and execute in parallel. String tools include `trim`, `lower`, `upper`, `regexp_replace`, and `split`; date tools include `to_date`, `to_timestamp`, `year`, `month`, `datediff`, and `date_format`. Arrays and structs can be accessed with column expressions such as `col("items")[0]` and `col("address.city")`. Parse dates with an explicit format when input is not ISO-like, and verify the session time zone for timestamp workflows. Handle invalid values with `try_to_timestamp` where supported by your Spark version, or explicitly count and quarantine parse failures.

## Retail Example
For product label `"  Fresh APPLES "`, use `trim` and `lower` to produce `"fresh apples"`. For order date `"2026-09-30"`, parse it as a date and derive year `2026` and month `9`. Do both with Spark expressions so the transformation scales beyond a local Python loop.

### Retail Questions and Answers
1. What is the normalized product label? **`fresh apples`.**
2. Which functions derive the year and month? **`year(parsed_date)` and `month(parsed_date)`.**
3. Why inspect failed date parses? **Malformed values can silently become null and disappear from downstream date logic.**

## Banking Assignment
Normalize synthetic merchant names by trimming whitespace and applying a consistent case. Parse ISO-8601 transaction timestamps, derive posting date and month, and select a nested card field from a struct. Report parse failures and explain how time zone choice could affect transactions near midnight.
