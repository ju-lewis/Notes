

## Series
A series is a one-dimensional array-like object containing:
1. An array of data
2. An associated array of labels called the index
### Instantiation:
```python
# Example:
sales_list = [1.2, 9.5, 3.4, 6.5]
series = pd.Series(sales_list)
```

### Useful attributes / methods:
- `series.index` - returns the index 'array'
- `series.values` - returns the value 'array'
- `series.mean()` - computes the overall mean
- `series.sum()` - sums all values in the series
- `series.loc(predicate)` - finds values that match the predicate
	- `series.loc(sales_series < 5)`
	- `series.loc("str_index_2")`
- `series.iloc(slice)` - finds values by index
	- `series.iloc(0:2)`

### Modifying Index Field
An index doesn't need to be an integer!

```python
string_index = ["str_index_1", 
				"str_index_2", 
				"str_index_3", 
				"str_index_4"]

series.index = string_index
```




## DataFrames
DataFrames are similar to 2D arrays.

### DataFrame Indexing Cheat Sheet:
`df[col_name]` - to project a single column (returns series)
`df[[col1, col2]]` - to project multiple columns (returns dataframe)
`df.loc[df[col] == value]` - selects records based on a predicate **(MUST BE A SERIES)**
`df.iloc[]` - selects records based on predicates on their index
``


### Instantiation

```python
import pandas as pd


sales_df = pd.DataFrame({"tickets_sold": tickets_sold,
						 "max_capacity": max_capacity})

sales_df["tickets_sold"] # Print a single column
sales_df[ ["tickets_sold", "max_capacity"] ] # Multiple

# We can use .loc here as well
sales_df.loc[sales_df["tickets_sold"] < 100000]

```


### Writing/Reading CSV File

```python
sales_df = pd.read_csv("booking_summary.csv")

# This WILL create an index column
sales_df.to_csv("booking_summary.csv")

# This won't create the index column
sales_df.to_csv("booking_summary.csv", index=False)
```

### Useful attributes and methods
- `df.head(num_rows: int)`
- `df.tail(num_rows: int)`


### Performing Operations on Records
You can directly perform arithmetic operations on DataFrame rows:
```python
# Print the unsold tickets for each entry
print(sales_df["max_capacity"] - sales_df["tickets_sold"])
```
