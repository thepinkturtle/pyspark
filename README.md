
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
```df.printSchema()```