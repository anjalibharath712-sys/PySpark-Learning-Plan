# Day 1: Get Started

## Goals
- Explain what PySpark is and when distributed processing is useful.
- Install PySpark and create a local `SparkSession`.

## Learn
Read the [PySpark overview](https://spark.apache.org/docs/latest/api/python/index.html), [quickstart](https://spark.apache.org/docs/latest/api/python/getting_started/quickstart.html), and [installation guide](https://spark.apache.org/docs/latest/api/python/getting_started/install.html).

## Practice
1. Create and activate a Python virtual environment, then install PySpark.
2. Start a `SparkSession` in a script or notebook and print `spark.version`.
3. Create a DataFrame from dictionaries; call `show()` and `printSchema()`.
4. Stop the session cleanly.

## Deliverable
A runnable script that creates a local Spark session and displays a DataFrame. Record your Python, Java, and Spark versions.

## Topic Notes
PySpark is the Python interface to Apache Spark. Use Spark when data volume, throughput, or parallel processing needs exceed a single-process workflow; for small data, pandas or plain Python can be simpler. A `SparkSession` is the entry point to DataFrame and SQL work. `master("local[2]")` runs locally with two worker threads and is for practice, not a cluster deployment. A DataFrame is a distributed, schema-bearing table, not a Python list.

Spark transformations describe work; actions such as `show`, `count`, and `collect` request results and trigger execution. Keep large results distributed; `collect()` transfers every row to the Python driver and can exhaust its memory.

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.master("local[2]").appName("learning-day-1").getOrCreate()
orders = spark.createDataFrame([
	("R101", 2, 15.0),
	("R102", 1, 10.0),
	("R103", 4, 10.0),
], ["order_id", "quantity", "unit_price"])
orders.show()
orders.printSchema()
spark.stop()
```

## Retail Example
The sample orders above represent point-of-sale transactions. Their line totals are 30.00, 10.00, and 40.00. In this example, `show()` is an action that lets you inspect these small practice rows.

### Retail Questions and Answers
1. How many orders are in the sample? **3**, using `orders.count()`.
2. What is the total sales amount before tax? **80.00**, calculated as `sum(quantity * unit_price)`.
3. Which operation should not be used to return a huge production dataset to Python? **`collect()`**.

## Banking Assignment
Create a `SparkSession` and a DataFrame for three fictional account transactions with `transaction_id`, `account_id`, `transaction_type`, and `amount`. Print the schema and sample rows, count transactions, and total the amounts. Explain why you should not collect the full transaction history to the driver. Use synthetic data only; never put real account or customer information in practice files.
