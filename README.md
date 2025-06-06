# Coffee Store Sales Analysis using Python

## Project Overview

**Project Title**: Coffee Store Sales Analysis  
**Level**: Intermediate  

This project analyzes sales data from two coffee outlets using Python. Each dataset was cleaned separately and then combined for analysis. Standard columns such as month, year, and day name were added to enrich the data before exporting. The goal is to uncover sales insights and enhance Python skills through practical data analysis.

![Logo](Logo.jpg)

## Objectives

1. **Set up the libraries**: Install and import all the libraries.
2. **Import Data**: Import data using various methods with the help of Pandas.
3. **Data Cleaning**: Data Cleaning.
4. **Data Export**: .
5. **Data Transformation**: Develop complex queries to analyze and retrieve specific data.
6. **Chats and Reports**: Develop complex queries to analyze and retrieve specific data.
7. **Additional**: Develop complex queries to analyze and retrieve specific data.

## Project Structure

### 1. Set up the libraries

- **Install Library**: install some of the most important libraries.
```python
# Install Libraries

!pip install pandas
!pip install numpy
!pip install matplotlib
!pip install seaborn
```    
- **Import Library**: Call Libraries for the using.

```python
# Import Libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### 2. Import Data

- **Import CSV file**
```python
df = pd.read_csv(r'path')
```
- **Import Excel file**
```python
df = pd.read_excel(r"path")
```
- **Import from SQL database**
```python
!pip install mysql-connector-python

import mysql.connector as sql
conn = sql.connect(
    host="localhost",
    user="root",
    password="@**a***2",
    use_pure = True,
    database ='megha'
)

data = "select * from student"
import pandas as pd
df = pd.read_sql(data, conn)

print(df) or df
```
- **Import from Web**
```python

```

### 3. Data Cleaning

#### Data Inspection
```python
# Display the entire dataset
df

# Show the first 10 rows of the dataset
df.head(10)

# Show the last 10 rows of the dataset
df.tail(10)

# Return the number of rows and columns (tuple format)
df.shape

# Display the column names of the dataset
df.columns

# Display information including column names, non-null counts, data types, and memory usage
df.info()

# Show statistical summary of numerical columns (mean, std, min, max, etc.)
df.describe()
```

#### Modify Data Types
```python
# Display the data types of each column
df.dtypes

# Convert specified columns to new data types
df = df.astype({
    'date': 'datetime64[ns]',
    'datetime': 'datetime64[ns]',
    'cash_type': 'object',
    'card': 'object',
    'money': 'float64',
    'coffee_name': 'object'
})
```
#### Create New Columns

- Direct method
```python
df['time_only'] = df['datetime'].dt.time # Extract only the time part from the 'datetime' column

df['outlet'] = "outlet1" # Create a new column 'outlet' with the same value "outlet1" for all rows

# Create 'month', 'week_number', and 'day_name' columns from the 'date' column

df["month"] = df["date"].dt.strftime("%b %y") # Format month as 'Jan 24' (short month name and year)

df['week_number'] = df['date'].dt.isocalendar().week # Extract ISO week number

df["day_name"] = df["date"].dt.strftime("%a") # Get abbreviated day name (e.g., 'Fri')

# %B: Full month name (e.g., "January"), %Y: Four-digit year (e.g., "2024"), 
# %d: Day of the month (01-31), %D: Date in MM/DD/YY format (e.g., "03/15/24")
```
- Insert method
```python
# Insert 'time' column at column index 1
df.insert(1, "time", df['datetime'].dt.time)

# Insert 'outlet' column at column index 3 with the same value ("outlet1") for all rows
df.insert(3, "outlet", "outlet1")
```

#### Remove Columns
```python
# For dropping a single column
df = df.drop(columns=['datetime'])

# For dropping multiple columns
df = df.drop(columns=['datetime', 'only_time'])
```

#### Rename Columns
```python
# Single Rename
df.rename(columns={
    'time_only': 'time'
},  inplace=True)

# Multi rename
df.rename(columns={
    'time_only': 'time', 
    'cash_type': 'mop', 
    'card': 'card_details', 
    'money': 'amount', 
    'coffee_name': 'product'
}, inplace=True)
```

#### Update Columns
```python
# Single cell/ Conditional update
df.loc[0, "cash_type"] = "UPI"

# Multi cell update
df['cash_type'] = "UPI"

```

#### Combine two data sets
```
df = pd.concat([df, df2], axis = 0).reset_index(drop=True)

# axis=0 refers to rows, and axis=1 refers to columns
```

#### Missing data Handle

```
# Returns True/False for each cell
df.isnull()

# Count of missing data in the column
df['card'].isnull().sum()

# Count of nulls in each column
df.isnull().sum()

# Rows with at least one null
df[df.isnull().any(axis=1)]
```

#### Missing data remove

```python
# Drop rows with any NaNs
df.dropna(inplace=True)

# Drop columns with any NaNs
df.dropna(axis=1, inplace=True)

# 0 = rows & 1 = columns

# Drop rows where all values are NaN
df.dropna(how='all', inplace=True)

# You can only use two values for how:

# any: Drop the row or column if any values are NaN.
# all: Drop the row or column only if all values are NaN.

# Drop rows if NaN in specific columns
df.dropna(subset=['card', 'money'], inplace = True)
```

#### Filling data remove
```python
# Fill NaNs with a specific value
df.fillna('value', inplace=True)

# Forward fill
df.fillna(method='ffill', inplace=True)

# Backward fill
df.fillna(method='bfill', inplace=True)

# Fill with mean/median/mode
df['col'].fillna(df['col'].mean())


```

### 4. Export Data through various methods 

- **Export CSV file**
```python
df.to_csv('output.csv', index=False)
```

- **Export excel file**
```python
df.to_excel('output.xlsx', index=False)
```

- **Clipboard**
```python
df.to_clipboard(index=False)
```

- **Export Json file**
```python
df.to_json('output.json', orient='records', lines=True)

# Orient can be 'records', 'split', 'index', 'columns', 'values', etc.
# Add lines=True for newline-delimited JSON.
```

- **Export HTML file**
```python
df.to_html('output.html', index=False)
```
### 5. Data Transformation

#### 1. Data Analysis & Findings
- **Total Revenue**

```python
Total_revenue = df['amount'].sum()

Total_revenue
```

- **Total Sales**
```python
Total_Sales = df['amount'].count()
Total_Sales

or

df['amount'].count()
```

- **Avg. amount per Sales**
```python
Total_Sales = df['amount'].count()
Total_Sales

or

df['amount'].count()
```

- **Highest Ordered product**
```python

```

- **Highest Revenue Product**
```python

```

- **Revenue by Outlet**
```python

```

- **Revenue mode of payment wise**
```python
df[df['mop'] == 'card']['amount'].sum(), df[df['mop'] == 'cash']['amount'].sum()
```

- **Sales mode of payment wise**
```python
df[df['mop'] == 'card']['amount'].count(), df[df['mop'] == 'cash']['amount'].count()
```

- **Monthly Sales**
```python
monthly_sales = df.groupby('month')['amount'].sum().reset_index()
```

- **Top Ordering Day of the Week**
```python

```

#### 2. Data Sorting

- **Sorting Data**:
```python
df.sort_values(by='money', ascending=False, inplace=True)

df.sort_values(by=['money', 'date'], ascending=[False, True], inplace=True)
```

#### 2. Data Grouping

- **Grouping Data**:
```python
# Group by one column, aggregate one column
df.groupby('mop')['amount'].sum()

# Group by one column, aggregate multiple columns
df.groupby('mop')[['amount', 'discount']].sum()

df.groupby('mop').agg({
    'amount': 'sum',
    'discount': 'mean'
})

# Group by multiple columns, aggregate one column
df.groupby(['region', 'mop'])['amount'].sum()

# Group by multiple columns, aggregate multiple columns
df.groupby(['region', 'mop']).agg({
    'amount': ['sum', 'mean'],
    'discount': ['sum', 'max']
})

```

#### 2. Charts

**Work in Progress....**

## Advanced py Operations

### 1. Pivot

```python
# Basic Pivot Table
pd.pivot_table(df, values='amount', index='outlet', columns='mop', aggfunc='sum')

#Pivot Table with Multiple Aggregations
pd.pivot_table(df, 
               values=['amount', 'discount'], 
               index='region', 
               columns='mop', 
               aggfunc={'amount': 'sum', 'discount': 'mean'})

# Add Totals
pd.pivot_table(df, 
               values='amount', 
               index='region', 
               columns='mop', 
               aggfunc='sum', 
               margins=True)

```

### 2. Interpolation

### 3. Eval

## Conclusion

This project demonstrates the use of Python for coffee sales analysis, currently utilizing libraries like Pandas for data manipulation, analysis, and basic visualization. It establishes a strong foundation for data-driven insights, with plans to integrate additional libraries such as NumPy and Matplotlib in future stages. The project is a work in progress, continuously evolving to deepen analytical capabilities and enhance Python proficiency.
