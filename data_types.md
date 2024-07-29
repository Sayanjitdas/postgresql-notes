# Data Types in SQL

## What are data types? 

Data types are classifications that define the kind of value a field (or column) can contain within a table in a database. It defines the type of data the field can hold, such as integer data, character data, monetary data, date and time data, binary strings, and so on.


## Data types in PostgreSQL

## Boolean

The boolean data type can store two values: `True` or `False`. There’s also a third Unknown state, which is represented by `Null`. It’s used for storing unknown or non applicable values. The boolean data type takes one byte of storage. Boolean data types are often used with logical operators such as `AND`,`OR`, and `NOT`.


### Character strings

These are collections of alphanumeric characters (letters, numbers, and special characters) and can be of fixed or variable length. Examples of character string data types in PostgreSQL include Char, Varchar, and Text.

- `Character varying(n)`: Also known as Varchar, stores variable-length character strings of up to n characters in length. If no value is specified for n, the size is unlimited.

- `Character(n)`: It’s similar to character varying but stores strings of exactly n characters in length. If the string is shorter in size than n characters, it will be padded with spaces to make it n characters long.

- `Text`: It stores character strings of unlimited length.


### Numeric
Numeric data types are used for storing numeric values. They can store whole numbers, decimal numbers, and floating point numbers. This data type is often used for storing financial information or measurements. They can be used in mathematical operators such as +, -, *, and /.

Numeric data types in PostgreSQL include `SmallInt`, `Integer`, `BigInt`, `Decimal`, `Numeric`, `Real`, `Double Precision`, `SmallSerial`, `Serial`, and `BigSerial`.

- `Smallint`: This data type stores integers (between -32,768 and 32,767). It takes 2 bytes of storage.

- `Integer`: This data type stores whole numbers (between -2,147,483,648 and 2,147,483,647). It takes 4 bytes of storage.

- `BigInt`: This data type stores whole numbers (between -9,223,372,036,854,775,808 and 9,223,372,036,854,775,807). It takes 8 bytes of storage.

- `Decimal or Numeric`: It stores decimal numbers (numbers with a fractional component). The decimal data type can store up to 131,072 digits before and up to 16,383 digits after the decimal point. The Decimal and Numeric data types are interchangeable, so we can use either when we need to store a numeric value.

- `Real`: It stores floating point numbers (numbers with a fractional component) with an accuracy of 6 decimal places. It takes 4 bytes of storage.

- `Double`: It stores floating point numbers with an accuracy of 15 decimal places. It takes 8 bytes of storage.

- `SmallSerial`: It stores integers (between 1 and 32,767) that are automatically incremented by the database. It takes 2 bytes of storage.

- `Serial`: It stores integers (between 1 and 2,147,483,647) that are automatically incremented by the database. It takes 4 bytes of storage.

- `BigSerial`: It stores integers (between 1 and 9,223,372,036,854,775,807) that are automatically incremented by the database. It takes 8 bytes of storage.


### Date/time types
This stores date and time values. Date/time data types in PostgreSQL include `Date`, `Timestamp`, `TimestamptZ`, `Interval`, and `Time`.

- `Date`: It stores date values (year, month, day). The range of values for the date data type is 4713 BC to 5874897 AD. It takes 4 bytes of storage.

- `Time`: It stores time values. It takes 4 bytes of storage.

- `Timestamp`: This data type stores date and time values (year, month, day, hour, minute, second). The range of values for the Timestamp data type is 4713 BC to 294276 AD. It takes 8 bytes of storage.

- `TimestampZ`: It’s similar to Timestamp but includes a time zone component. It takes 8 bytes of storage.

- `Interval`: It stores interval values. Interval values represent a period. Interval values are stored as the number of days, hours, minutes, seconds, and milliseconds. The interval data type takes 8 bytes of storage.


### Array
Array data types store an ordered collection of elements. We can use it to store a list of values of the same data type. Arrays can be of any data type, including built-in, user-defined, and enumerated types.

To create an array column, we use the following syntax:
```
CREATE TABLE <table_name> (
    <column_name> <data_type>[]
);
```

Here, <table_name> is the table’s name, <column_name> is the column’s name, and <data_type> is the data type of the array.

To insert an array value into an array column, we use the following syntax:

```
INSERT INTO <table_name> (<column_name>)
VALUES ('{<value1>,<value2>,..}');
```

An example of using an array data type in PostgreSQL is given below:

```
CREATE TABLE Product (
	id  INTEGER PRIMARY KEY, 
	name TEXT UNIQUE,
	price NUMERIC(7,2),
  hashtag VARCHAR(50)[],
	quantity INTEGER
);

INSERT INTO
  Product (id, name, price, hashtag, quantity)
VALUES
  (
    1,
    'iPhone',
    999.99,
    ARRAY ['Apple','iPhone','Smartphone'],
    5
  ), 
  (
    2,
    'iPad',
    399.99,
    ARRAY ['Apple','iPad','Tablet'],
    12
  );

SELECT id, name, price, quantity, hashtag FROM Product;

SELECT '\n' AS " "; -- Adding new line

SELECT 
  hashtag[1] AS "tag #1", 
  hashtag[2] AS "tag #2", 
  hashtag[3] AS "tag #3"
FROM 
  Product 
WHERE 
  id = 2; 
```

### Enumeration
Enumerated data types represent a set of discrete values. We can enumerate data types to store values that we can select from a list of options.

The `CREATE TYPE` statement creates the enumerated data types.

```
CREATE TYPE status_type AS ENUM ('active', 'inactive');
```

This example creates an enumerated data type called status_type. We can use it to store the values 'active' and 'inactive'

The following is an example of how to use the `status_type` data type:

```
CREATE TABLE Users (
    id serial PRIMARY KEY,
    name VARCHAR(255),
    status status_type
);

\dt
```

### Miscellaneous data types

In addition to the data types listed above, a few others are worth mentioning. These data types include:

- `JSON`: It stores JSON (JavaScript Object Notation) data. JSON is a text format that we can use to represent structured data.

- `XML`: It stores XML data. XML is a markup language that we can use to store and transport data.

- `Geometry`: PostgreSQL also provides several data types for storing geometric data. The Geometric data types represent two-dimensional spatial objects such as points, lines, and polygons.

- `Networking`: PostgreSQL provides several data types for storing network addresses. Network address data types store IP addresses and media access control (MAC) addresses.

- `Large object`: PostgreSQL also provides a data type for storing large objects. Large object data types store binary data such as images, videos, and documents.