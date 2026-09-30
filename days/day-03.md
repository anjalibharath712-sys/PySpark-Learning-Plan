# Day 3: Work with DataFrames

## Goals
- Create DataFrames from local data and inspect their schemas.
- Distinguish inferred schemas from explicitly defined schemas.

## Learn
Use the [PySpark quickstart](https://spark.apache.org/docs/latest/api/python/getting_started/quickstart.html) and [DataFrame API reference](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/dataframe.html).

## Practice
1. Create an employee or orders DataFrame using Python dictionaries or tuples.
2. Define a `StructType` schema with suitable names and data types.
3. Compare the explicit schema with inferred types on equivalent data.
4. Inspect rows with `show()`, `limit()`, and `printSchema()`; avoid collecting large data to the driver.

## Deliverable
A script that creates two related DataFrames with explicit schemas and displays their schemas and sample rows.

## Topic Notes
A schema names each column and assigns its Spark SQL type. Explicit schemas make data contracts predictable and avoid relying on type inference from a limited or inconsistent sample. Common types include `StringType`, `LongType`, `IntegerType`, `DoubleType`, `BooleanType`, `DateType`, `TimestampType`, and `DecimalType`. Prefer `DecimalType` for fixed-precision currency. A `StructType` contains ordered `StructField` definitions; each field also records whether nulls are allowed.

```python
from pyspark.sql.types import StructField, StructType, StringType, IntegerType, DecimalType

schema = StructType([
	StructField("sku", StringType(), False),
	StructField("quantity", IntegerType(), False),
	StructField("unit_price", DecimalType(8, 2), False),
])
```

Schema inference is convenient for exploration but can misclassify mixed values or depend on sampled rows. Inspect the schema with `printSchema()` and check representative rows before transforming data.

## Retail Example
An order-line table can use `order_id: StringType`, `sku: StringType`, `quantity: IntegerType`, and `unit_price: DecimalType(8, 2)`. Treat a SKU such as `"000418"` as a string so leading zeros are preserved; represent a price such as 12.50 with decimal precision rather than binary floating point.

### Retail Questions and Answers
1. Why is `sku` a string instead of an integer? **It is an identifier, not a number to calculate with; leading zeros matter.**
2. Which type is appropriate for a fixed-precision price? **`DecimalType`, with precision and scale chosen for the domain.**
3. What is a risk of inferring the schema from a few rows? **Later values may have different types or precision, causing inconsistent results or failed reads.**

## Banking Assignment
Define an explicit schema for synthetic ledger rows containing `transaction_id`, `account_id`, `posted_at`, `currency`, and `amount`. Keep identifiers and currency codes as strings, use a timestamp for `posted_at`, and choose a decimal type for `amount`. Create sample data, inspect the schema, and explain why inference could be unsafe for IDs and monetary values.
