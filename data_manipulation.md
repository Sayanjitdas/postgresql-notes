## Data Manipulation Commands

### The `INSERT` statement

Syntax of insert statement

```
INSERT INTO
  <table_name> (<column_1>, <column_2>, ... <column_n>)
VALUES
  (<value_1>, <value_2>, <value_3>, ... <value_n>)
```

Inserting multple rows

```
INSERT INTO <table_name> (<column_1>, <column_2>, .... <column_n>)
VALUES 
    (<value1_1>, <value1_2>, <value1_3>, ... <value1_n>),
    (<value2_1>, <value2_2>, <value2_3>, ... <value2_n>),
    ...
    (<value3_1>, <value3_2>, <value3_3>, ... <value3_n>);

```

It’s also possible to insert a row into a table without specifying any values, like so:

```
INSERT INTO 
  <table_name>
DEFAULT VALUES;
```
This statement inserts a new row into the table_name table with default values for each column. This is only useful if all of the columns in the table have a default value specified.


Some examples of `INSERT`

```
INSERT INTO
  Employee (id, first_name, last_name, hire_date, salary)
VALUES
  (1, 'John', 'Doe', '2010-01-01', 50000.00);
```

```
INSERT INTO
  Employee (id, first_name, last_name, hire_date, salary)
VALUES
  (2, 'Jane', 'Smith', '2012-04-15', 55000.00),
  (3, 'Jack', 'Jones', '2011-12-03', 40000.00);
```

It’s also possible to insert data from another table into a table. It can be done using the following syntax:

```
INSERT INTO
  Alumni
SELECT
  *
FROM
  Employee;
```

This will insert every row from the Employee table into the Alumni table, assuming that the Alumni table has the same structure (i.e., the same columns in the same order) as the Employee table.

If the Alumni table does not have the same structure as the Employee table, you would need to specify the columns explicitly, like this:

```
INSERT INTO Alumni (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM Employee;
```


### Update query

The UPDATE command changes the data in a table. The syntax for the UPDATE command is as follows:

```
UPDATE
  <table_name>
SET
  <column1> = <value1>,
  <column2> = <value2>...
WHERE
  <condition>

```
Examples

```
UPDATE
  Employee
SET
  salary = 15000,
  department = 'Sales'
WHERE
  name = 'John';
```

### Using the ON UPDATE CASCADE option

If we want to update all of the data from a table and all of the tables that depend on those tables, we can define the ON UPDATE CASCADE option in the FOREIGN KEY constraint, as given below:

```
ALTER TABLE Manager 
  ADD CONSTRAINT emp_mgr_fk FOREIGN KEY (emp_id) REFERENCES Employee (id)
  ON UPDATE CASCADE;

\d Manager
```

 The `ALTER TABLE` command adds a constraint for the foreign key relationship between the `Employee` and `Manager` tables. This constraint specifies that any rows in the `Employee` table that reference a row in the `Manager` table must have an `id` value that matches one of the values in the Manager table. The `ON UPDATE CASCADE` clause specifies that any rows in the Manager table that are updated will also result in updating any matching rows in the Employee table.

> It’s important to exercise caution when using ON UPDATE CASCADE as it can sometimes lead to unexpected and potentially damaging consequences. In particular, we should always test our UPDATE statement on a small subset of data before running it on the entire table.

### Using the RETURNING keyword with the UPDATE command

We can use the RETURNING keyword with the UPDATE command to return the updated data. To update the salary of John to 20% and return the updated data, we can use the following UPDATE statement:

```
UPDATE
  Employee
SET
  salary = 15000 * 1.2
WHERE
  name = 'John' RETURNING salary;
```

> RETURNING keyword can be used with insert update and delete as well.

### Deleting some data from a table

```
DELETE FROM
 <table_name>
WHERE
 <condition>;
```

Example

```
DELETE FROM
  Employee
WHERE
  id = 1;
```

To delete all data from the table

```
DELETE FROM Employee;
```

### Using the ON DELETE CASCADE option

If we want to delete all of the data from a table and all of the tables that depend on those tables, we can define the ON DELETE CASCADE option in the FOREIGN KEY constraint, as given below:

```
ALTER TABLE 
    MANAGER 
ADD 
    CONSTRAINT fk_emp_manager FOREIGN KEY (emp_id) REFERENCES Employee (id)
    ON DELETE CASCADE;

\d Manager
```

The `ALTER TABLE` command is used to add a constraint for the foreign key relationship between the `Employee` and `Manager` tables. This constraint specifies that any rows in the `Employee` table that reference a row in the `Manager` table must have an `id` value that matches one of the values in the Manager table. The `ON DELETE CASCADE` clause specifies that any rows in the `Manager` table that’s deleted will also result in the deletion of any matching rows in the `Employee` table.

> It’s important to exercise caution when using ON DELETE CASCADE as it can sometimes lead to unexpected and potentially damaging consequences. In particular, we should always test our DELETE statement on a small subset of data before running it on the entire table.