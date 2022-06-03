# Group
- groupBy
```python
result = my_df.groupBy("col_name_of_choice")
```

- join
```python
# most common is an inner join
# given two datasets with atleast one matching column
# the '[]' syntax will remove/discard duplicating the matching column

result = my_left_df.join(my_right_df, ["my_matching_col"])
```
# agg functions
- agg(): used primarly in the ```groupby()``` to create super cool clean aggregation columns
```python
# given a dataframe tags that contains tags for movies that looks like:
#+------+-------+-----------------+-------------------+
#|userId|movieId|              tag|          timestamp|
#+------+-------+-----------------+-------------------+
#|     2|  60756|            funny|2015-10-24 19:29:54|
#|     2|  60756|  Highly quotable|2015-10-24 19:29:56|
#|     2|  60756|     will ferrell|2015-10-24 19:29:52|
#|     2|  89774|     Boxing story|2015-10-24 19:33:27|
#|     2|  89774|              MMA|2015-10-24 19:33:20|
#|     2|  89774|        Tom Hardy|2015-10-24 19:33:25|
#|     2| 106782|            drugs|2015-10-24 19:30:54|
#|     2| 106782|Leonardo DiCaprio|2015-10-24 19:30:51|
#+------+-------+-----------------+-------------------+

tags.groupby("movieId").agg(
    f.collect_set("tag").alias("tags"),`#alias's just temporarily rename the col
    f.count("tag").alias("tag_count"),
    f.collect_set("userId").alias("users"),
    f.count("userId").alias("user_count"),
    f.min("timestamp").alias("first_tagged_date"),
    f.max("timestamp").alias("last_tagged_date")
).sort(f.col("tag_count").desc()).show() # sort desc'ing is often done this way

# You'll end up with something like the following
#+-------+--------------------+---------+--------------------+----------+-------------------+-------------------+
#|movieId|                tags|tag_count|               users|user_count|  first_tagged_date|   last_tagged_date|
#+-------+--------------------+---------+--------------------+----------+-------------------+-------------------+
#|    296|[foul language, r...|      181|[103, 474, 424, 599]|       181|2006-01-14 02:16:41|2017-06-26 05:58:14|
#|   2959|[powerful ending,...|       54|[474, 424, 599, 435]|        54|2006-01-14 02:17:14|2017-06-26 06:02:47|
#|    924|[music, atmospher...|       41|          [474, 599]|        41|2006-01-15 23:33:55|2017-06-26 06:00:27|
#|    293|[friendship, orga...|       35|     [474, 166, 599]|        35|2006-01-24 21:20:19|2017-06-26 05:49:52|
#|   7361|[arthouse, atmosp...|       34|[477, 474, 424, 1...|        34|2006-01-14 02:30:08|2018-05-02 17:40:11|
#|   1732|[Philip Seymour H...|       32|          [474, 599]|        32|2006-01-26 20:17:41|2017-06-26 05:51:48|
#|   4878|[surreal, atmosph...|       29|[477, 474, 424, 1...|        29|2006-01-14 02:29:41|2018-05-02 17:36:42|
#+-------+--------------------+---------+--------------------+----------+-------------------+-------------------+

```
