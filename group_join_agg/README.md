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
