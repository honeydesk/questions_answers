## Question: In simpleimputer (sklearn), there is a parameter 'strategy'. There is an information written for 'strategy' parameter as follows : "strategy : str or Callable, default=’mean'" . Now, tell the meaning of callable. Give me an example to make it understood.

A **callable** is any object in Python that can be **called like a function**, which means it is expected to take an array of data and return a single value for imputation. 
Using a callable allows you to customize the imputation strategy beyond the built-in options.

### What a Callable Does in This Context

When you pass a callable to `strategy`, `SimpleImputer` will **apply this function to each column (or row if `axis=1`) with missing values**. 
The function should return a single value for each column, which `SimpleImputer` will use to fill in the missing values for that column.

### Example: Using a Custom Callable as a Strategy

Suppose you want to fill missing values in a way that is not covered by the default options, such as **imputing with the 90th percentile** of each column. You can pass a custom function that calculates this percentile as a callable to the `strategy` parameter.

Here’s an example:

```python
import numpy as np
from sklearn.impute import SimpleImputer

# Custom function to calculate the 90th percentile
def percentile_90(column):
    return np.nanpercentile(column, 90)

# Create SimpleImputer with custom strategy (callable)
imputer = SimpleImputer(strategy=percentile_90)

# Example data with missing values
data = np.array([[1, 2, np.nan],
                 [4, np.nan, 6],
                 [7, 8, 9],
                 [np.nan, 10, 11]])

# Apply the imputer
imputed_data = imputer.fit_transform(data)

print(imputed_data)
```

### Explanation
1. **Define the Callable**: We define a custom function, `percentile_90`, that calculates the 90th percentile of a column. This function will be applied to each column that contains missing values.
2. **Pass Callable to `strategy`**: We initialize `SimpleImputer` with `strategy=percentile_90`, so `SimpleImputer` will use the result of this function for imputing missing values.
3. **Transform the Data**: When calling `fit_transform` on the data, `SimpleImputer` fills missing values in each column using the 90th percentile of non-missing values in that column.

### Output
This custom strategy fills in missing values based on the 90th percentile, giving you flexibility for different imputation techniques not provided by default in `scikit-learn`.
  

  

  
