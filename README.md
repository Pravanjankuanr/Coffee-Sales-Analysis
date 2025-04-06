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

```
# Import Libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### 2. Import Data

- **Import CSV file**: .
```
df = pd.read_csv(r'path')
```
- **Import Excel file**: .
```
df = pd.read_excel(r"path")
```
- **Import from SQL database**: .
```
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
```

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

```
# Direct method to create new columns

df['time_only'] = df['datetime'].dt.time # Extract only the time part from the 'datetime' column

df['outlet'] = "outlet1" # Create a new column 'outlet' with the same value ("outlet1") for all rows

# Create 'month', 'week_number', and 'day_name' columns from the 'date' column

df["month"] = df["date"].dt.strftime("%b %y") # Format month as 'Jan 24' (short month name and year) 

df['week_number'] = df['date'].dt.isocalendar().week # Extract ISO week number

df["day_name"] = df["date"].dt.strftime("%a") # Get abbreviated day name (e.g., 'Fri')

# Insert method to create new columns

df.insert(1, "time", df['datetime'].dt.time) # Insert 'time' column at column index 1

df.insert(3, "outlet", "outlet1") # Insert 'outlet' column at column index 3 with the same value ("outlet1") for all rows

# %B: Full month name (e.g., "January"), %Y: Four-digit year (e.g., "2024"), 
# %d: Day of the month (01-31), %D: Date in MM/DD/YY format (e.g., "03/15/24")
```

#### Remove Columns
```
# For dropping a single column
df = df.drop(columns=['datetime'])

# For dropping multiple columns
df = df.drop(columns=['datetime', 'only_time'])
```

#### Rename Columns
```
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
-- for one value
df
```

#### Combine two data sets
```
df = pd.concat([df, df2]).reset_index(drop=True)
```

### 4. Export Data various method 

```python
df.to_csv('output.csv', index=False)
```

### Data Transformation

#### 1. Data Analysis & Findings

- **Total Revenue**:

```python
Total_revenue = df['amount'].sum()

Total_revenue
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

## Advanced py Operations

**Task 13: Identify Members with Overdue Books**  

```sql
SELECT 
    ist.issued_member_id,
    m.member_name,
    bk.book_title,
    ist.issued_date,
    -- rs.return_date,
    CURRENT_DATE - ist.issued_date as over_dues_days
FROM issued_status as ist
JOIN 
members as m
    ON m.member_id = ist.issued_member_id
JOIN 
books as bk
ON bk.isbn = ist.issued_book_isbn
LEFT JOIN 
return_status as rs
ON rs.issued_id = ist.issued_id
WHERE 
    rs.return_date IS NULL
    AND
    (CURRENT_DATE - ist.issued_date) > 30
ORDER BY 1
```


**Task 14: Update Book Status on Return**  
Write a query to update the status of books in the books table to "Yes" when they are returned (based on entries in the return_status table).


```sql

CREATE OR REPLACE PROCEDURE add_return_records(p_return_id VARCHAR(10), p_issued_id VARCHAR(10), p_book_quality VARCHAR(10))
LANGUAGE plpgsql
AS $$

DECLARE
    v_isbn VARCHAR(50);
    v_book_name VARCHAR(80);
    
BEGIN
    -- all your logic and code
    -- inserting into returns based on users input
    INSERT INTO return_status(return_id, issued_id, return_date, book_quality)
    VALUES
    (p_return_id, p_issued_id, CURRENT_DATE, p_book_quality);

    SELECT 
        issued_book_isbn,
        issued_book_name
        INTO
        v_isbn,
        v_book_name
    FROM issued_status
    WHERE issued_id = p_issued_id;

    UPDATE books
    SET status = 'yes'
    WHERE isbn = v_isbn;

    RAISE NOTICE 'Thank you for returning the book: %', v_book_name;
    
END;
$$


-- Testing FUNCTION add_return_records

issued_id = IS135
ISBN = WHERE isbn = '978-0-307-58837-1'

SELECT * FROM books
WHERE isbn = '978-0-307-58837-1';

SELECT * FROM issued_status
WHERE issued_book_isbn = '978-0-307-58837-1';

SELECT * FROM return_status
WHERE issued_id = 'IS135';

-- calling function 
CALL add_return_records('RS138', 'IS135', 'Good');

-- calling function 
CALL add_return_records('RS148', 'IS140', 'Good');

```




**Task 15: Branch Performance Report**  
Create a query that generates a performance report for each branch, showing the number of books issued, the number of books returned, and the total revenue generated from book rentals.

```sql
CREATE TABLE branch_reports
AS
SELECT 
    b.branch_id,
    b.manager_id,
    COUNT(ist.issued_id) as number_book_issued,
    COUNT(rs.return_id) as number_of_book_return,
    SUM(bk.rental_price) as total_revenue
FROM issued_status as ist
JOIN 
employees as e
ON e.emp_id = ist.issued_emp_id
JOIN
branch as b
ON e.branch_id = b.branch_id
LEFT JOIN
return_status as rs
ON rs.issued_id = ist.issued_id
JOIN 
books as bk
ON ist.issued_book_isbn = bk.isbn
GROUP BY 1, 2;

SELECT * FROM branch_reports;
```

**Task 16: CTAS: Create a Table of Active Members**  
Use the CREATE TABLE AS (CTAS) statement to create a new table active_members containing members who have issued at least one book in the last 2 months.

```sql

CREATE TABLE active_members
AS
SELECT * FROM members
WHERE member_id IN (SELECT 
                        DISTINCT issued_member_id   
                    FROM issued_status
                    WHERE 
                        issued_date >= CURRENT_DATE - INTERVAL '2 month'
                    )
;

SELECT * FROM active_members;

```


**Task 17: Find Employees with the Most Book Issues Processed**  
Write a query to find the top 3 employees who have processed the most book issues. Display the employee name, number of books processed, and their branch.

```sql
SELECT 
    e.emp_name,
    b.*,
    COUNT(ist.issued_id) as no_book_issued
FROM issued_status as ist
JOIN
employees as e
ON e.emp_id = ist.issued_emp_id
JOIN
branch as b
ON e.branch_id = b.branch_id
GROUP BY 1, 2
```

**Task 18: Identify Members Issuing High-Risk Books**  
Write a query to identify members who have issued books more than twice with the status "damaged" in the books table. Display the member name, book title, and the number of times they've issued damaged books.    


**Task 19: Stored Procedure**
Objective:
Create a stored procedure to manage the status of books in a library system.
Description:
Write a stored procedure that updates the status of a book in the library based on its issuance. The procedure should function as follows:
The stored procedure should take the book_id as an input parameter.
The procedure should first check if the book is available (status = 'yes').
If the book is available, it should be issued, and the status in the books table should be updated to 'no'.
If the book is not available (status = 'no'), the procedure should return an error message indicating that the book is currently not available.

```sql

CREATE OR REPLACE PROCEDURE issue_book(p_issued_id VARCHAR(10), p_issued_member_id VARCHAR(30), p_issued_book_isbn VARCHAR(30), p_issued_emp_id VARCHAR(10))
LANGUAGE plpgsql
AS $$

DECLARE
-- all the variabable
    v_status VARCHAR(10);

BEGIN
-- all the code
    -- checking if book is available 'yes'
    SELECT 
        status 
        INTO
        v_status
    FROM books
    WHERE isbn = p_issued_book_isbn;

    IF v_status = 'yes' THEN

        INSERT INTO issued_status(issued_id, issued_member_id, issued_date, issued_book_isbn, issued_emp_id)
        VALUES
        (p_issued_id, p_issued_member_id, CURRENT_DATE, p_issued_book_isbn, p_issued_emp_id);

        UPDATE books
            SET status = 'no'
        WHERE isbn = p_issued_book_isbn;

        RAISE NOTICE 'Book records added successfully for book isbn : %', p_issued_book_isbn;


    ELSE
        RAISE NOTICE 'Sorry to inform you the book you have requested is unavailable book_isbn: %', p_issued_book_isbn;
    END IF;
END;
$$

-- Testing The function
SELECT * FROM books;
-- "978-0-553-29698-2" -- yes
-- "978-0-375-41398-8" -- no
SELECT * FROM issued_status;

CALL issue_book('IS155', 'C108', '978-0-553-29698-2', 'E104');
CALL issue_book('IS156', 'C108', '978-0-375-41398-8', 'E104');

SELECT * FROM books
WHERE isbn = '978-0-375-41398-8'

```



**Task 20: Create Table As Select (CTAS)**
Objective: Create a CTAS (Create Table As Select) query to identify overdue books and calculate fines.

Description: Write a CTAS query to create a new table that lists each member and the books they have issued but not returned within 30 days. The table should include:
    The number of overdue books.
    The total fines, with each day's fine calculated at $0.50.
    The number of books issued by each member.
    The resulting table should show:
    Member ID
    Number of overdue books
    Total fines

## Conclusion

This project demonstrates the application of SQL skills in creating and managing a library management system. It includes database setup, data manipulation, and advanced querying, providing a solid foundation for data management and analysis.
