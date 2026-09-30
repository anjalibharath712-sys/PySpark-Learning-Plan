# Day 19: Build the Capstone

## Goals
- Design a complete batch pipeline with clear inputs, transformations, and outputs.
- Combine DataFrame, SQL, file, and testing skills from previous days.

## Project
Choose a public or generated dataset. Build a pipeline that reads raw data, applies an explicit schema, validates records, cleans and transforms fields, joins a lookup table, and writes an analytics-ready Parquet dataset partitioned on a useful field.

## Practice
1. Define input assumptions, output schema, and quality rules before coding.
2. Keep transformations in testable functions and isolate input/output paths.
3. Add at least three quality checks and two automated tests.
4. Inspect the query plan and make one evidence-based performance improvement.

## Deliverable
A working pipeline, sample output, and a README section explaining how to run it and what the output contains.
