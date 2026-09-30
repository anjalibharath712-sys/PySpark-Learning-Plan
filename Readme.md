# 20-Day PySpark Learning Plan

A practical, project-based path from Python and Spark fundamentals to building and tuning a complete data pipeline. Plan for about 60-90 minutes per day. Use a local Spark installation for the exercises; a managed Spark environment is optional.

## Before You Start

- Be comfortable with Python basics, functions, collections, and virtual environments.
- Have access to a terminal, a code editor, and a recent Java runtime supported by your chosen Spark version.
- Install PySpark in a virtual environment with `pip install pyspark`, following the official [installation guide](https://spark.apache.org/docs/latest/api/python/getting_started/install.html).
- Keep each day's code and notes in a small practice project. Use a public CSV dataset for exercises, or generate sample data yourself.

## Daily Lessons

| Day | Topic | Lesson |
| --- | --- | --- |
| 1 | Spark and PySpark setup | [Day 1: Get Started](days/day-01.md) |
| 2 | Spark architecture | [Day 2: Understand Spark](days/day-02.md) |
| 3 | DataFrames and schemas | [Day 3: Work with DataFrames](days/day-03.md) |
| 4 | Selecting and transforming columns | [Day 4: Transform Data](days/day-04.md) |
| 5 | Filtering, sorting, and nulls | [Day 5: Clean Rows and Values](days/day-05.md) |
| 6 | Aggregations and grouping | [Day 6: Summarize Data](days/day-06.md) |
| 7 | Joins and set operations | [Day 7: Combine DataFrames](days/day-07.md) |
| 8 | Spark SQL | [Day 8: Query with Spark SQL](days/day-08.md) |
| 9 | Dates, strings, and nested data | [Day 9: Use Built-in Functions](days/day-09.md) |
| 10 | Files and data formats | [Day 10: Read and Write Data](days/day-10.md) |
| 11 | RDDs and execution concepts | [Day 11: Learn RDD Fundamentals](days/day-11.md) |
| 12 | Execution plans and lazy evaluation | [Day 12: Inspect Query Plans](days/day-12.md) |
| 13 | Partitioning and shuffles | [Day 13: Manage Partitions](days/day-13.md) |
| 14 | Performance tuning | [Day 14: Tune Spark Jobs](days/day-14.md) |
| 15 | UDFs and reusable logic | [Day 15: Extend PySpark Carefully](days/day-15.md) |
| 16 | Testing and data quality | [Day 16: Test Data Pipelines](days/day-16.md) |
| 17 | Structured Streaming | [Day 17: Process Streaming Data](days/day-17.md) |
| 18 | MLlib introduction | [Day 18: Build a Basic ML Pipeline](days/day-18.md) |
| 19 | Capstone pipeline design | [Day 19: Build the Capstone](days/day-19.md) |
| 20 | Capstone completion and review | [Day 20: Validate and Present](days/day-20.md) |

## Finish Line

By the end, you should be able to build a tested batch pipeline that reads raw data, validates and transforms it, joins reference data, writes partitioned output, and explains its execution plan and performance choices. You will also have tried the core ideas behind streaming and ML pipelines.

Use the official [PySpark documentation](https://spark.apache.org/docs/latest/api/python/index.html) as your reference. Spark behavior and APIs can vary by version, so check the documentation for the version you install.

