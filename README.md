# SQL_Reference

### Order of SQL Query Execution

1. **FROM**: The tables to be queried are identified.
2. **WHERE**: Filters the rows based on specified conditions.
3. **GROUP BY**: Groups rows sharing a property.
4. **HAVING**: Filters groups based on specified conditions.
5. **SELECT**: Selects the columns to be returned, and this is where aliases are assigned.
6. **ORDER BY**: Orders the result set.
7. LIMIT

**Filtering text**

`WHERE IN` WHERE column_name IN (value1, value2, ...);

`Between`

`LIKE` - `NOT LIKE` Ad%  Ad_ 

`Ad_` followed by exactly one character

**`SELECT A.*`** statement in SQL is used to select all columns from a table

**NULL values**

`where is null ||| where in not null` 

```sql
SELECT * FROM Customers
WHERE Address IS NULL;
```

**`COUNT()`** function does not count **`NULL`** values (non missing value) 

**Aggregate functions**

AVG(), SUM(), MIN(), MAX(), COUNT() 

Aggregate functions return a single value for a set of values

**Arithmetic** operations

(+, - , / , *) work on individual values within rows (return a value for each row.)

**Aliases** 

Can’t use `Aliases` in `Where` clause due to order of execution

```sql
SELECT Salary + Bonus AS TotalCompensation
FROM Employees
WHERE TotalCompensation > 50000;
```

This query will result in an **error** because **`TotalCompensation`** is an alias defined in the **`SELECT`** clause, which is processed after the **`WHERE`** clause.

To use the alias in a condition, you can use a **subquery**:

**Sorting results**

ASCending - A Z

1 - 10

```sql
SELECT * FROM Products
ORDER BY Price ASC;
#the lowest to the highest.
```

DESCending - Z A

10 - 1

```sql
SELECT * FROM Orders
ORDER BY OrderDate DESC;
# the most recent orders first.
```

**Grouping data** 

When you use an aggregate function in a **`SELECT`** statement, every column in the **`SELECT`** list must either be part of an aggregate function or included in the **`GROUP BY`** clause.

```sql
SELECT Department, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY Department;
```

- **`HAVING`**vs **`WHERE`** clause
    - To use the **`WHERE`** clause need to filter the rows before the aggregation.
    - **`WHERE`** cannot be used with aggregate functions like **`SUM`**,
    - you would need to use a subquery or a Common Table Expression (CTE)

**CASE statements** 

categorizing data

filtering data 

aggregating data

```sql
SELECT EmployeeID,
Salary,
CASE
	WHEN Salary > 50000 THEN 'High'
	WHEN Salary BETWEEN 30000 AND 50000 THEN 'Medium'
	ELSE 'Low'
	END AS SalaryCategory
FROM Employees;
```

**subquery**

A subquery, also known as a nested query or inner query, is a query within another SQL query. Subqueries are used to retrieve data that will be used in the main query as a condition or for further processing. They can be placed in various parts of a SQL statement, such as the **`SELECT`**, **`FROM`**, **`WHERE`**, and **`HAVING`** clauses.

**Subquery in `WHERE` Clause**

```sql
SELECT EmployeeID, FirstName, LastName
FROM Employees
WHERE DepartmentID IN (SELECT DepartmentID FROM Departments WHERE LocationID = 1700);
```
**A Common Table Expression (CTE)**

a temporary result set that you can reference within a `SELECT`, `INSERT`,` UPDATE`, or `DELETE` statement. CTEs are particularly useful for simplifying complex queries and improving readability. 
Recursive CTE
CTEs can also be recursive, which is useful for hierarchical data, such as organizational charts or tree structures.
Basic Syntax
```sql
WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)
SELECT column1, column2
FROM cte_name
WHERE another_condition;
```

Joins 

- **`UNION`**: Removes duplicate rows from the combined result set.
- **`UNION ALL`**: Includes all rows, including duplicates, in the combined result set.
