# Day 16: Test Data Pipelines

## Goals
- Write deterministic tests for transformations and data-quality rules.
- Separate transformation logic from file I/O and Spark session setup.

## Learn
Follow the [PySpark testing guide](https://spark.apache.org/docs/latest/api/python/getting_started/testing_pyspark.html) and [testing helpers reference](https://spark.apache.org/docs/latest/api/python/reference/pyspark.testing.html).

## Practice
1. Extract a transformation into a function that accepts and returns a DataFrame.
2. Create small input and expected DataFrames with explicit schemas.
3. Test values, schema, null handling, and duplicate-key behavior.
4. Add tests for empty input and one invalid-data case.

## Deliverable
A small automated test suite that checks expected output and an important edge case.
