
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

- Show the current schema ```df.printSchema()```
  - if rows are truncating and you want to see them then use the ```truncate=False``` parameter  

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

- function.explode(): will take something like an array and make a new row for each item in the array see the example below
starting with this:

```python
# Given a data.csv with multiple values in one column seperated by a '|' symbol 
# +-------+----------------------------------+-------------------------------------------+
# |movieId|title                             |genres                                     |
# +-------+----------------------------------+-------------------------------------------+
# |1      |Toy Story (1995)                  |Adventure|Animation|Children|Comedy|Fantasy|
# |2      |Jumanji (1995)                    |Adventure|Children|Fantasy                 |
# |3      |Grumpier Old Men (1995)           |Comedy|Romance                             |
# |4      |Waiting to Exhale (1995)          |Comedy|Drama|Romance                       |
# |5      |Father of the Bride Part II (1995)|Comedy                                     |
# +-------+----------------------------------+-------------------------------------------+

movie_genre = (
    movies
    .withColumn("genres_array", f.split("genres", "\|"))
    # split the values in the column 'genres' into an array of values on the '|' symbol
    
    .withColumn("genre", f.explode("genres_array"))
    # make a new row for every value in the genres_array column and store the new value in the genre column
    
    .select("movieId", "title", "genre")
)

# Resulting in this:
# +-------+-----------------------+---------+
# |movieId|title                  |genre    |
# +-------+-----------------------+---------+
# |1      |Toy Story (1995)       |Adventure|
# |1      |Toy Story (1995)       |Animation|
# |1      |Toy Story (1995)       |Children |
# |1      |Toy Story (1995)       |Comedy   |
# |1      |Toy Story (1995)       |Fantasy  |
# |2      |Jumanji (1995)         |Adventure|
# |2      |Jumanji (1995)         |Children |
# |2      |Jumanji (1995)         |Fantasy  |
# |3      |Grumpier Old Men (1995)|Comedy   |
# |3      |Grumpier Old Men (1995)|Romance  |
# +-------+-----------------------+---------+
```

