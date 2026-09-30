# Day 12: Inspect Query Plans

## Goals
- Explain lazy evaluation and identify actions that trigger execution.
- Read the basic sections of a physical query plan.

## Learn
Review [DataFrame explain](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.DataFrame.explain.html) and [Spark SQL performance tuning](https://spark.apache.org/docs/latest/sql-performance-tuning.html).

## Practice
1. Build transformations and note they do not execute until an action runs.
2. Call `explain("formatted")` before and after adding a filter or projection.
3. Identify scans, exchanges, joins, and aggregates in the plan.
4. Open the Spark UI and connect the plan to the job and stages from an action.

## Deliverable
A short annotated query plan with one observation about where data is read or shuffled.

## Topic Notes
Spark records DataFrame transformations as a logical plan instead of executing each line immediately. Catalyst analyzes and optimizes that plan, then Spark creates a physical plan. `explain("formatted")` shows readable physical-plan nodes; `explain("extended")` includes logical and physical plans. Look for scans, pushed filters, projections, exchanges (shuffle boundaries), join strategies, and aggregates. Adaptive Query Execution may revise parts of the plan at runtime, so the final plan can differ from the initial one. Actions such as `count`, `show`, or `write` trigger execution.

## Retail Example
For a sales DataFrame, apply a date filter, select `store_id` and `amount`, group by store, and sum. Call `explain("formatted")` before running the aggregate. Expect a scan and projection/filter operations, then an exchange may appear before the final aggregate because rows must be grouped by key.

### Retail Questions and Answers
1. Does constructing `sales.filter(...)` alone run a Spark job? **No; it creates a plan.**
2. What does an `Exchange` commonly indicate? **A redistribution of rows, often a shuffle.**
3. Which method inspects a readable physical plan? **`DataFrame.explain("formatted")`.**

## Banking Assignment
Filter synthetic payments to one date range, select the fields needed for a branch-level aggregate, and call `explain("formatted")`. Identify the scan, filter, aggregate, and any exchange. Trigger the query with an action, then compare the plan with the job/stage view in the Spark UI.
