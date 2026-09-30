# Day 15: Extend PySpark Carefully

## Goals
- Know when built-in Spark functions are preferable to Python UDFs.
- Create a UDF only when the required logic cannot be expressed otherwise.

## Learn
Review the [PySpark UDF API](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.functions.udf.html) and [built-in functions](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/functions.html).

## Practice
1. Implement a simple transformation with built-in functions.
2. Implement equivalent logic as a Python UDF and compare readability and plans.
3. Set and verify the return type explicitly for the UDF.
4. Document edge cases and test null inputs.

## Deliverable
A tested example showing the built-in solution first, plus a UDF only if it demonstrates a real need.
