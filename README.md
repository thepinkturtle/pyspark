
### Tips tricks and notes for quick pyspark reference
- Create spark session 
```python
from pyspark.sql import SparkSession

# standard way to make a spark session
spark = SparkSession.builder.appName("MyFirstCSVLoad").getOrCreate()
```

- load data
  - can use ```inferSchema=True``` however you wont guarantee type safety so use it only for dataset exploration
```python
# replace "example.csv" with your dataset .csv file of choice likewise change the schema to the dataset schema too
df = spark.read.csv(path="example.csv", 
                    header=True, 
                    sep=',',
                    quote='"',
                    schema="userId INT, movieId INT, rating DOUBLE, timestamp INT") #schema DDL/DML 
# will lose rows if not match schema but ensures type safety
```
- Show first n rows of data
```df.show(5)```

- Show the current schema
  - if rows are truncating and you want to see them then use the 'truncate=False' parameter 
```df.printSchema()```

- Renaming columns
```python
df = (
    df
    .withColumnRenamed("timestamp", "timestamp_unix") #rename col to timestamp_unix
)
````

- function.from_unixtime(): convert to human readable time
```python
df = (
    df
    .withColumn("timestamp", f.from_unixtime("your_unix_timestamp_col")) 
    # run opperation and create a new col with results from 'from_unixtime' function
)
```

- function.to_timestamp(): convert type to timestamp
```python
df = (
    df
    .withColumn("timestamp", f.to_timestamp("timestamp"))
    # convert column type to timestamp type
)
```
