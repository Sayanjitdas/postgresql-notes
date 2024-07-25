# Data Definition language

**Content**
- [Creating database](#creating-a-database)
- [Creating tables](#creating-tables)
- [Creating tables with PK and FK](#creating-tables-with-primary-key)
- [Truncate tables](#truncate-table)
- [Deleting and renaming a database](#deleting-a-database)
- [Renaming and Deleting a table](#renaming-a-table)
- [Adding and dropping Columns](#adding-columns)
- [Setting and dropping default values for columns](#setting-default-values-for-columns)
- [Renaming Columns](#renaming-columns)
- [Adding Constraint](#adding-constraint)
- [Dropping Constraint](#dropping-a-constraint)

### Creating a database

`CREATE DATABASE <database name>;`

`\l <database name>` shows the database details in psql 

`\x` creates an expanded format in psql

### Creating tables

```
CREATE TABLE <table_name> (
    <column_name> <data_type>, 
    <column_name> <data_type>, 
    <column_name> <data_type>,
    ..., 
    <column_name> <data_type>);
```

`\d <table name>` to display tables

### Creating tables with primary key
```
CREATE TABLE Customer (
    id INTEGER PRIMARY KEY, 
    name VARCHAR(255), 
    dob DATE
);
```
> We use the PRIMARY KEY column constraint to create a table with a primary key. A primary key is a column or a set of columns uniquely identifying a row in a table.

### Creating tables with foreign key
```
CREATE TABLE Order (
    id INTEGER,
    customer_id INTEGER, 
    product_id INTEGER, 
    FOREIGN KEY (customer_id) REFERENCES Customer(id),
);
```
> A foreign key is a column or a set of columns in one table that provides a link between data in two tables. A foreign key value must match an existing primary key value in the other table. PostgreSQL will raise an error if we try to insert or update a row in the child table with values that don’t exist in the parent table. PostgreSQL uses the FOREIGN KEY column constraint to create a foreign key.

### Truncate table
`TRUNCATE TABLE <table_name>;`

> If we want to delete all the data in the table and reset the serial primary key to 1 we use truncate.

### Deleting a database

`DROP DATABASE <database_name>;`

> Before deleting a database, make sure to back up any critical data. Be careful when using this command in production, as it can’t be undone. Same goes for truncate as well

`DROP DATABASE IF EXISTS customer_db;`
>The DROP DATABASE command with the IF EXISTS clause will only drop the database if it exists. Otherwise, it will return a notice. This can be useful in cases where we aren’t sure if the database exists or not.

>The `DROP DATABASE customer_db;` command will return an error as the database does not exist. The `DROP DATABASE IF EXISTS customer_db;` command will not return an error. Instead, we’ll see a notice like NOTICE: database "customer_db" does not exist, skipping. This can be particularly useful in automated scripts where we want the command to succeed regardless of whether the database is present. This helps to make the operation idempotent, meaning it can be executed multiple times without different outcomes.

### Renaming a database

`ALTER DATABASE <old_name> RENAME TO <new_name>;`

>The ALTER DATABASE will only change the name of the database and not its contents. Also, we must make sure to update any references to the database in our code or queries to reflect the new name.

### Renaming a table
`ALTER TABLE <old_name> RENAME TO <new_name>;`
>This will only change the name of the table and not its contents. Also, we have to make sure to update any references to the table in our code or queries to reflect the new name.

### Dropping a table

`DROP TABLE <table_name>;`
>The DROP TABLE command will permanently delete the table and any data stored in it. We can also use IF EXIST clause as well with Drop table like `DROP TABLE IF EXISTS <table_name>;`


### Adding Columns
```
ALTER TABLE 
  <table_name> 
ADD COLUMN 
  <column_name> <datatype>;
```

### Drop Columns
```
ALTER TABLE <table_name> 
  DROP COLUMN <column_name>;
```

> We can use the IF EXISTS clause with Drop columns like `ALTER TABLE <table_name> DROP Column IF EXISTS phone_number;`

### Setting default values for columns
```
ALTER TABLE 
  <table_name> 
ALTER COLUMN 
  <column_name> 
SET 
  DEFAULT <default_value>;
```

### Dropping default values for columns
```
ALTER TABLE 
  <table_name> 
ALTER COLUMN 
  <column_name> DROP DEFAULT;
```
>Be careful when using this command, as it may result in unexpected changes to existing data. It’s always a good idea to back up our data before making any changes.


### Renaming columns
```
ALTER TABLE 
  <table_name> RENAME COLUMN <old_column_name> TO <new_column_name>;
```

### Adding constraint
```
ALTER TABLE 
  <table_name> 
ADD 
   CONSTRAINT <constraint_name> <constraint_type>(<column_name>);  
```

The code widget below provides commands to add the following constraints:
- `PRIMARY_KEY`
- `UNIQUE`
- `NOT NULL`
- `DEFAULT`
- `CHECK`
- `FOREIGN_KEY`

```
ALTER TABLE
  Customer
ADD
  CONSTRAINT customer_pk PRIMARY KEY (id); -- Adding PRIMARY KEY

ALTER TABLE
  Customer
ADD
  CONSTRAINT unique_email UNIQUE (email); -- Adding UNIQUE constraint

ALTER TABLE
  Customer
ALTER COLUMN
  id
SET
  NOT NULL; -- Adding NOT NULL constraint

ALTER TABLE 
  Customer 
ALTER COLUMN 
  dob 
SET 
  DEFAULT '2000-01-01'; -- Adding DEFAULT contstraint

ALTER TABLE
  Customer
ADD
  CONSTRAINT check_customer_id CHECK (id > 0); -- Adding CHECK constraint

ALTER TABLE
  Users
ADD
  CONSTRAINT user_customer_fk FOREIGN KEY (id) REFERENCES Customer (id); 
--- Adding FOREIGN KEY constraint

\d Customer 

SELECT '\n' AS " "; -- Adding new line

\d Users
```

### Dropping a constraint

```
ALTER TABLE 
  <table_name> DROP CONSTRAINT <constraint_name>; 
```