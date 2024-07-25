# Postgresql cheat sheet and notes

## SQL Basics

### Creating a database

> `CREATE DATABASE <database name>`

> `\l <database name>` shows the database details in psql 

> `\x` creates an expanded format in psql

### Creating tables
> `CREATE TABLE <table_name> (
    <column_name> <data_type>, 
    <column_name> <data_type>, 
    <column_name> <data_type>,
    ..., 
    <column_name> <data_type>)`