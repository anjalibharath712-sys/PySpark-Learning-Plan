# Day 2: Understand Spark

## Goals
- Describe the driver, executors, jobs, stages, and tasks.
- Recognize why Spark distributes work and where data movement costs time.

## Learn
Read the [Spark cluster overview](https://spark.apache.org/docs/latest/cluster-overview.html) and the [RDD programming guide](https://spark.apache.org/docs/latest/rdd-programming-guide.html).

## Practice
1. Run a DataFrame transformation followed by an action such as `count()`.
2. Open the Spark UI at the local URL printed by Spark, usually `http://localhost:4040`.
3. Find the job, stage, and task created by the action.
4. Sketch how a driver coordinates work with executors.

## Deliverable
A diagram or note describing the path from an action to completed tasks, with one example of work that can require a shuffle.

## Topic Notes
The driver creates the Spark application, builds the logical work plan, schedules tasks, and coordinates results. Executors run tasks and can cache partitions. A job is generally started by an action; Spark divides it into stages at shuffle boundaries, and tasks process partitions within stages. In local mode, the driver and executor work run on your machine, so this is a learning setup rather than a distributed cluster.

DataFrames are evaluated lazily: transformations build a plan, while an action such as `count()` or a write executes it. A shuffle redistributes data across partitions, commonly for grouping, sorting, or joins. Shuffles involve network and disk I/O and are important to spot in the Spark UI and query plan.

## Retail Example
Suppose a retailer groups 10 million sales rows by `store_id` and `department`. The input is split into partitions; executors aggregate their partitions, then Spark redistributes matching keys so final totals can be combined. Calling `show()` on the grouped result triggers the job; defining the `groupBy` alone does not.

### Retail Questions and Answers
1. Which component schedules the work? **The driver.**
2. Does `groupBy(...).sum(...)` execute immediately? **No; it is a transformation until an action requests results.**
3. Why can grouping require a shuffle? **Rows with the same grouping keys must be brought together across partitions.**

## Banking Assignment
For synthetic payment events, group transaction amounts by `branch_id` and `transaction_type`. Draw the driver, executors, partitions, and shuffle boundary; identify which operation triggers execution and name the likely shuffle stage. In the Spark UI, locate the job and stage created by an action on your grouped result.
