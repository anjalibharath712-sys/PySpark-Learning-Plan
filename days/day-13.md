# Day 13: Manage Partitions

## Goals
- Explain how partitions affect parallelism and task size.
- Distinguish repartitioning from coalescing and recognize shuffle costs.

## Learn
Review the [RDD programming guide](https://spark.apache.org/docs/latest/rdd-programming-guide.html) and [Spark SQL performance tuning](https://spark.apache.org/docs/latest/sql-performance-tuning.html).

## Practice
1. Inspect a DataFrame's partition count with `spark_partition_id()` and `count()`.
2. Compare `repartition` and `coalesce` for a chosen partition count.
3. Inspect the query plan and Spark UI to find whether a shuffle occurred.
4. Write output at different partition counts and observe the number of output files.

## Deliverable
An experiment log with partition counts, observed tradeoffs, and a reasoned output-file strategy.
