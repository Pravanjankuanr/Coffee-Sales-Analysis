# Coffee Store Sales Analysis using Python

## Project Overview

**Project Title**: Coffee Store Sales Analysis  
**Level**: Intermediate  

This project demonstrates the implementation of a Library Management System using SQL. It includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries. The goal is to showcase skills in database design, manipulation, and querying.

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

- **Import CSV file**: .
```python
df = pd.read_csv(r'path')
```
- **Import Excel file**: .
```python
df = pd.read_excel(r"path")
```
- **Import from SQL database**: .
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
- **Import from Web**: .
```python

```

### 3. Data Cleaning

#### Data Inspection

```python
df # Display the entire dataset

df.head(10) # Show the first 10 rows of the dataset

df.tail(10) # Show the last 10 rows of the dataset

df.shape # Return the number of rows and columns (tuple format)

df.columns # Display the column names of the dataset

df.info() # Display information including column names, non-null counts, data types, and memory usage

df.describe() # Show statistical summary of numerical columns (mean, std, min, max, etc.)
```
#### Modify Data Types

```python
df.dtypes # Display the data types of each column

-- Convert specified columns to new data types
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

df['outlet'] = "outlet1" # Create a new column 'outlet' with the same value ("outlet1") for all rows

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
df = pd.concat([df, df2]).reset_index(drop=True)
```
#### Missing data Handle

```
df['card'].isnull().sum()
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

- **Clipboard file**
```python
df.to_clipboard(index=False)
```

- **Export Json file**: .
```python
df.to_json('output.json', orient='records', lines=True)

# Orient can be 'records', 'split', 'index', 'columns', 'values', etc.
# Add lines=True for newline-delimited JSON.
```

- **Export HTML file**: .
```python
df.to_html('output.html', index=False)
```
### Data Transformation

#### 1. Data Analysis & Findings

- **Total Revenue**:

```python
Total_revenue = df['amount'].sum()

Total_revenue
```

- **Sorting Data**:

```python
df.sort_values(by='money', ascending=False, inplace=True)

df.sort_values(by=['money', 'date'], ascending=[False, True], inplace=True)
```

- **Total Sales**:

```python
Total_Sales = df['amount'].count()
Total_Sales

or

df['amount'].count()
```

- **Total Sales mop wise**:

```python
Total_Sales = df['amount'].count()
Total_Sales

or

df['amount'].count()
```

#### 2. Charts
**Work in Progress....**
## Advanced py Operations

## Conclusion

This project demonstrates the application of SQL skills in creating and managing a library management system. It includes database setup, data manipulation, and advanced querying, providing a solid foundation for data management and analysis.
