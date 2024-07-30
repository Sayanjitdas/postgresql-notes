## Retrieving Data from Tables

Content:
- [Select query](#select-query)
- [DISTINCT](#distinct)
- [ORDER_BY](#order-by)
- [GROUP_BY](#group-by)
- [HAVING](#having-clause)


### Select query

The most basic form of the SELECT statement looks like this

```
SELECT
  *
FROM
  <table_name>;
```
It will select all of the columns in the table_name table. The wildcard character * represents all the columns.

We can select specific columns like below

```
SELECT
  <field_1>,
  <field_2>,
  ...
  <field_n>
FROM
  <table_name>
WHERE
  <condition>
```
Here, <field_1>, <field_2>, ... represents the names of the columns we want to select and <table_name> is the name of the table from which we want to fetch data.


We can use the `WHERE` clause to filter the returned rows. For example, to see employees whose salary is greater than 40,000, we could use the following query:

```
SELECT
  *
FROM
  Employee
WHERE
  salary > 40000;
```

### DISTINCT

We use the DISTINCT clause to return unique values. For example, to know how many different departments we have, we could use the following query:

```
SELECT
  DISTINCT department
FROM
  Employee;

```
This statement returns a list of all the unique departments in the Employee table. It’s important to note that we can only use the DISTINCT clause with a single column.


### ORDER BY

We use `ORDER BY` to sort the returned rows. For example, to see a list of our employees ordered by salary, we could use the following query:

```
SELECT
  *
FROM
  Employee
ORDER BY
  salary;
```

This statement returns all the columns for all the rows in the Employee table, sorted by salary from lowest to highest.

We can return the data sorted by salary from highest to lower (reverse order), as follows:

```
SELECT
  *
FROM
  Employee
ORDER BY
  salary DESC;
```
The statement above will return all the rows sorted by salary in descending order (from highest to lowest).


### GROUP BY

The GROUP BY clause in SQL is used to group rows with identical values in specified columns, allowing for aggregate functions (like SUM, AVG) to be applied to each group, summarizing or computing data across these groups.

The list of some of the most common aggregate functions is given below:

| Function | Description |
|----------|-------------|
| AVG      | Returns the average value |
| COUNT    | Returns the number of rows|
| MAX      | Returns the maximum value |
| MIN      | Returns the minimum value |
| SUM      | Returns the sum of values |

For example, if we wanted to know the number of employees in each department, we could use the following query:

```
SELECT
  department,
  COUNT(*) as "Number of Employees"
FROM
  Employee
GROUP BY
  department;
```
The statement will return something like below:

```
department	Number of Employees
IT	        4
Marketing	1
HR	        2
Sales	    2
```

### HAVING clause

The HAVING clause is used to filter results after grouping them with the GROUP BY clause, allowing for conditions to be applied on groups. For instance, it can filter to show only departments with more than one employee.

```
SELECT
  department,
  COUNT(*) as "Number of Employees"
FROM
  Employee
GROUP BY
  department
HAVING
  COUNT(*) > 1;

```

This SQL statement returns the department and a count of all the employees in each department with more than one employee. The HAVING clause is very useful in conjunction with the GROUP BY clause and the aggregate functions. It allows us to filter out groups that don’t meet specific criteria.

We can also use the DISTINCT clause with aggregate functions. For example, if we wanted to know how many distinct salaries we have in each department, we could use the following query:

```
SELECT
  department,
  COUNT(DISTINCT salary)
FROM
  Employee
GROUP BY
  department;

```

This statement returns the department and a count of all the unique salaries in each department.

