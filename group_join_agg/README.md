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
#|     2| 106782|  Martin Scorsese|2015-10-24 19:30:56|
#|     7|  48516|     way too long|2007-01-25 01:08:45|
#|    18|    431|        Al Pacino|2016-05-01 21:39:25|
#|    18|    431|         gangster|2016-05-01 21:39:09|
#|    18|    431|            mafia|2016-05-01 21:39:15|
#|    18|   1221|        Al Pacino|2016-04-26 19:35:06|
#|    18|   1221|            Mafia|2016-04-26 19:35:03|
#|    18|   5995|        holocaust|2016-02-17 18:57:52|
#|    18|   5995|       true story|2016-02-17 18:57:59|
#|    18|  44665|     twist ending|2016-03-02 19:51:23|
#|    18|  52604|  Anthony Hopkins|2016-03-10 22:58:16|
#|    18|  52604|  courtroom drama|2016-03-10 22:58:31|
#+------+-------+-----------------+-------------------+
my_tags_df.groupby("")
```
