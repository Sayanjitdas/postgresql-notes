# Postgresql cheat sheet and notes

## SQL Basics

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

### TRUNCATE TABLE
`TRUNCATE TABLE <table_name>;`

> If we want to delete all the data in the table and reset the serial primary key to 1 we use truncate.

### Deleting a database

`DROP DATABASE <database_name>;`

> Before deleting a database, make sure to back up any critical data. Be careful when using this command in production, as it can’t be undone. Same goes for truncate as well

`DROP DATABASE IF EXISTS customer_db;`
>The DROP DATABASE command with the IF EXISTS clause will only drop the database if it exists. Otherwise, it will return a notice. This can be useful in cases where we aren’t sure if the database exists or not.

>The `DROP DATABASE customer_db;` command will return an error as the database does not exist. The `DROP DATABASE IF EXISTS customer_db;` command will not return an error. Instead, we’ll see a notice like NOTICE: database "customer_db" does not exist, skipping. This can be particularly useful in automated scripts where we want the command to succeed regardless of whether the database is present. This helps to make the operation idempotent, meaning it can be executed multiple times without different outcomes.