# Day 17: Process Streaming Data

## Goals
- Explain the Structured Streaming DataFrame model.
- Build a small streaming query with a checkpoint and output sink.

## Learn
Read the [Structured Streaming guide](https://spark.apache.org/docs/latest/streaming/index.html) and [PySpark streaming API](https://spark.apache.org/docs/latest/api/python/reference/pyspark.ss/index.html).

## Practice
1. Use the `rate` source or a local file source to produce sample events.
2. Apply a projection and aggregation, then write to the console sink.
3. Configure a checkpoint location and explain why it matters.
4. Observe the query lifecycle and stop it cleanly.

## Deliverable
A runnable streaming example with a checkpoint path and notes on its source, trigger, and sink.
