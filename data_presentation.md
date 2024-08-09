## Data presentation

Content
---
- [Limit clause](#limit-clause)
- [offset clause](#offset-clause)
- [order by clause](#order-by-clause)
- [Joins](#using-joins)
- [Different types of join](#different-types-of-joins)

### Limit clause

The LIMIT command limits the number of rows returned from a query.

```
SELECT
  <column(s)>
FROM
  <table_name>
LIMIT <count>;
```
The <count> specifies the number of rows to return.


### Offset clause

The OFFSET command is used to skip a certain number of rows before beginning to return results.

```
SELECT
  <column(s)>
FROM
  <table_name> 
OFFSET <number>;
```

The <number> specifies the number of rows to skip before beginning to return results.


We can use both the LIMIT and OFFSET commands together to return a certain number of rows starting at a specific row.

```
SELECT
  <column(s)>
FROM
  <table_name> 
LIMIT <count> [OFFSET] <number>;

```

The OFFSET is optional and defaults to 0 if not supplied.


if we wanted to return two rows starting at the 5th row, we’d use the following query:

```
SELECT
  *
FROM
  Employee
LIMIT 2 OFFSET 5;

```

### ORDER BY clause

We can use the ORDER BY command to control the order in which rows are returned.

```
SELECT
  <column(s)>
FROM
  <table_name>
ORDER BY
  <column_name> ASC | DESC;
```

>Note: The ORDER BY clause should always come at the end of our SELECT statement, after any other clauses such as WHERE or GROUP BY.


### Using joins

```
SELECT
  <columns>
FROM
  <table1> JOIN <table2> 
  ON <condition>;

```

```
SELECT
  Product.product_id AS pid,
  Product.product_name AS name,
  Product.price,
  Sales.sales_id as sid,
  Sales.quantity AS qty,
  Sales.date
FROM
  Product
  JOIN Sales ON Product.product_id = Sales.product_id;

```
Here, Product JOIN Sales means we want to join the Product table with the Sales table. The ON statement specifies the condition for joining; in this case, the product_id from the Product table must be equal to the product_id from the Sales table.


### Different types of joins

There are different types of JOIN commands available in PostgreSQL:

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN


**INNER JOIN**

The most straightforward kind of join is an INNER JOIN. This is the most common type of join, which returns rows when there’s a match in both tables.

```
SELECT
  Product.product_id AS pid,
  Product.product_name AS name,
  Product.price,
  Sales.sales_id as sid,
  Sales.quantity AS qty,
  Sales.date
FROM
  Product INNER JOIN Sales 
  ON Product.product_id = Sales.product_id;
```

The query above returns all the sales records for products listed in the Product and Sales table.

>In PostgreSQL, JOIN and INNER JOIN are the same .

**LEFT OUTER JOIN**

This type of join returns all the rows from the table on the left, even if there are no matches in the table on the right.

```
SELECT
  Product.product_id AS pid,
  Product.product_name AS name,
  Product.price,
  Sales.sales_id as sid,
  Sales.quantity AS qty,
  Sales.date
FROM
  Product LEFT JOIN Sales 
  ON Product.product_id = Sales.product_id;

```

This statement retrieves all the records from the Product table, and any matching records from the Sales table. The ON clause specifies the relationship between the tables using the product_id column. This is called a LEFT JOIN because all records from the left (first) table are returned, even if there are no matches in the right (second) table.

> LEFT JOIN and LEFT OUTER JOIN are the same in PostgreSQL.

**RIGHT JOIN**

A RIGHT JOIN includes all the rows from the right table, even if no matching values exist in the left table. Rows from the right table that don’t have matches in the left table will be filled with NULL values.

```
SELECT
  Product.product_id AS pid,
  Product.product_name AS name,
  Product.price,
  Sales.sales_id as sid,
  Sales.quantity AS qty,
  Sales.date
FROM
  Product RIGHT JOIN Sales 
  ON Product.product_id = Sales.product_id;
```
This statement retrieves all the records from the Sales table and any matching records from the Product table.

> PostgreSQL, RIGHT JOIN and RIGHT OUTER JOIN are the same.

**FULL JOIN**

A FULL JOIN includes all the rows from both tables, even if no matching values exist.

```
SELECT
  Product.product_id AS pid,
  Product.product_name AS name,
  Product.price,
  Sales.sales_id as sid,
  Sales.quantity AS qty,
  Sales.date
FROM
  Product FULL JOIN Sales 
  ON Product.product_id = Sales.product_id;
```

The statement above retrieves all the records from the Product and Sales tables, regardless of whether there are matching records in the other table.

>  In PostgreSQL, FULL JOIN and FULL OUTER JOIN are the same.

