
### Databricks
- In order to load a dataset into the tmp directory for ease of use later when changing absolute paths to relative ones do the following 
```python
# The dbfs path that you copied when the upload the data
dbfs_path = 'dbfs:/FileStore/shared_uploads/dlacrosse3@gatech.edu/nodes.txt'
local_path = 'file:///tmp/nodes.txt'

# Copy (cp) the file from dbfs to local file system in driver node
dbutils.fs.cp(dbfs_path, local_path)
```

- Then to load the data into a pandas dataframe do the following
```python
import pandas as pd
path_to_data = '/tmp/nodes.txt'
text_input = pd.read_csv(path_to_data, sep='\t', header=None)
text_input.head()
```
