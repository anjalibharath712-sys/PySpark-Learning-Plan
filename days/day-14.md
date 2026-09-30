# Day 14: Tune Spark Jobs

## Goals
- Identify common causes of slow Spark jobs.
- Apply practical tuning without guessing at configuration values.

## Learn
Read [Spark SQL performance tuning](https://spark.apache.org/docs/latest/sql-performance-tuning.html) and the [configuration guide](https://spark.apache.org/docs/latest/configuration.html).

## Practice
1. Pick a repeatable workload and establish a baseline runtime and query plan.
2. Project only needed columns and filter early; compare plan and runtime.
3. Inspect join strategies and test broadcast only when one side is demonstrably small.
4. Review shuffle partitions, caching, and file sizes; change one variable at a time.

## Deliverable
A before/after tuning note reporting the workload, change, and measured effect. Do not claim a speedup from a single noisy run.
