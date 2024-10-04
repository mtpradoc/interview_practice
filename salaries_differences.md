# Salaries Differences

Write a query that calculates the difference between the highest salaries found in the marketing and engineering deparments. Output just the absolute difference in salaries.

## Dataframes
db_employee
db_dept

Expected Output Type: pandas.DataFrame

db_employee
id: int64
first_name: object
last_name: object
salary: int64
department_id: int64
email: datetime64[ns]

db_dept
id: int64
department: object

```python
# Import your libraries
import pandas as pd

# Start writing code
db_employee.head()

# Step 1. Getting all the information into a single dataframe

# Merge dataframes
df = db_employee.merge(db_dept, how='left', left_on='department_id', right_on='id')

solution = abs(df[df['department'] == 'engineering']['salary'].max() - df[df['department'] == 'marketing']['salary'].max())

```
