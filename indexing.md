## Using indexing to Improve QUery Performance

Content
---
- [WHat is Indexing](#what-is-indexing)
- [Types of Indexing](#types-of-indexes)
- [Creating an Index](#creating-an-index)
- [Rebuilding an Index](#rebuilding-index)
- [Dropping an index](#dropping-an-index)



### What is Indexing?

An index in a database is a data structure that allows faster data retrievel from table. When we run a query, the database uses the index to quickly locate the request information instead of scanning through every row in the table. Postgresql indexes can significantly improve our database speed and efficiency. They do this by storing a sorted list of values for particular columns, allowing faster data lookup and retrieval.

It's important to note that creating an index comes at a cost - it takes up additional storage space and can slow down dara insertion and updates. Therefore, it's important to carefully assess the benefits of an index for a particular qury before creating one.

### Types of Indexes

- **B-Tree**: This is the most commonly used type of index in PostgreSQL. It’s useful for supporting queries on a range of data values (e.g., WHERE x > 5 AND x < 10) and can also support partial matches (e.g., WHERE first_name LIKE 'Joh%'). PostgreSQL automatically creates a B-tree index on primary key columns.

- **Hash**: This index type is best for equality matches (e.g., WHERE x = 5) and can’t support range queries or partial matches. Note that PostgreSQL automatically creates a Hash index on unique columns.

- **GiST**: This stands for Generalized Search Tree. These indexes can support a variety of data types, including geometric shapes, network addresses, and text search documents.

- **GIN**: This stands for Generalized Inverted Indexes. These are useful for indexing values in multiple rows, such as array values.

- **BRIN**: This stands for Block Range Indexes. They’re a type of index that PostgreSQL can use to efficiently query very large tables by only examining a small number of “representative” blocks in the table rather than the entire table.


### Creating an Index

```
CREATE INDEX <index_name> ON <table_name> (<column1>, <column2>, ...);
```

Here, <index_name> is the name we want to give the index, <table_name> is the name of the table to be indexed, and <column1>, <column2>, etc., are the columns to be included in the index.

Example:
```
CREATE INDEX idx_customer_fname_lname ON Customer (last_name, first_name);

\d+ idx_customer_fname_lname
```
To view information about the newly created idx_customer_name index, we can run the following command:
`\d+ idx_customer_name`

In addition to creating indexes on individual columns, PostgreSQL also allows for creating expression indexes, which index the result of an expression instead of a specific column value.

```
CREATE INDEX idx_customer_name ON Customer ((first_name || ' ' || last_name));
\d+ idx_customer_name
```

This can be especially useful for speeding up queries that involve calculations or other expressions. PostgreSQL also has the ability to automatically create and manage some types of indexes known as partial indexes and BRIN indexes.

```
CREATE INDEX idx_customer_brin ON Customer (id) WHERE id > 10; 
```

### Rebuilding Index

We use the REINDEX command to rebuild an index. This can be necessary if the index has become corrupted or is not used efficiently.

```
REINDEX INDEX <index_name>;
```
>Note: Rebuilding an index can take a while, and will temporarily lock the table it’s associated with. So it should be done during off-peak times or when there won’t be heavy usage of the table. Additionally, if we’re rebuilding, it might be worth considering dropping and recreating the index, as this can sometimes be more efficient. This can be done with the DROP INDEX and CREATE INDEX commands.

Overall, rebuilding or dropping and recreating indexes should not be done frequently, but can sometimes greatly improve the performance of our database. It’s important to regularly analyze our indexes and determine if any action needs to be taken.


### Dropping an Index

Deleting an existing index using the DROP INDEX statement is also possible.

```
DROP INDEX <index_name>;
```

For example:
```
DROP INDEX idx_customer_name;
```
