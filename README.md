
### Tips tricks and notes for quick pyspark reference
- load data
```python 
df = spark.read.csv(path="ratings.csv", 
                    header=True, 
                    sep=',',
                    quote='"',
                    schema="userId INT, movieId INT, rating DOUBLE, timestamp INT") # called a schema DDL/DML ensures type saftey
# will lose rows if not match schema but ensures type safety
```
