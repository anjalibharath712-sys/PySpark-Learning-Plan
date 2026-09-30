# Day 10: Read and Write Data

## Goals
- Read and write common file formats with explicit options.
- Understand why columnar formats and partitioned output matter.

## Learn
Review the guides for [CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html), [JSON](https://spark.apache.org/docs/latest/sql-data-sources-json.html), and [Parquet](https://spark.apache.org/docs/latest/sql-data-sources-parquet.html).

## Practice
1. Read CSV with a header, an explicit schema, and suitable parsing options.
2. Write cleaned data to Parquet and read it back.
3. Compare file sizes and schema behavior for CSV and Parquet on the same sample.
4. Partition output by a useful field and inspect the directory layout.

## Deliverable
A repeatable read-transform-write script with documented input and output paths and formats.

## Topic Notes
Spark reads and writes through `DataFrameReader` and `DataFrameWriter`. Provide an explicit schema when the data contract is known, and set format-specific options such as CSV `header`, `delimiter`, and `mode`. CSV is portable and human-readable but has weak type information; JSON supports nested records but can be verbose; Parquet is columnar, stores schema, and is usually efficient for analytical scans. Save modes include `error`/`errorifexists`, `append`, `overwrite`, and `ignore`; select them deliberately. `partitionBy` creates directory partitions and works best with useful, bounded-cardinality fields, not unique IDs.

```python
orders.write.mode("overwrite").partitionBy("sale_date").parquet("output/orders")
loaded = spark.read.parquet("output/orders")
```

## Retail Example
Read a CSV of point-of-sale rows with a known schema, normalize it, and write Parquet partitioned by sale month. Reading the Parquet output back should preserve the declared numeric and date types. Compare a projected query reading only `sku` and `quantity` from CSV versus Parquet to understand columnar reads.

### Retail Questions and Answers
1. Which format is a strong default for analytical Spark output? **Parquet, because it is columnar and preserves schema.**
2. Why not partition output by `transaction_id`? **Nearly every value would create a directory, producing excessive small partitions/files.**
3. What should be checked after a write/read round trip? **Schema, row counts, representative values, and the output directory layout.**

## Banking Assignment
Read synthetic ledger CSV with explicit timestamp and decimal fields; write the validated data to Parquet partitioned by posting month. Read it back and compare schema, row count, and total amount. Choose a save mode appropriate for a repeatable practice run, and explain why production financial records should not be silently overwritten.
