## Arithmetic and Comparison Operators in SQL

### Types of operators

- Arithmetic operators

- Comparison operators

- Logical operators


### Arithmatic operators

Arithmetic operators perform arithmetic operations on numeric data. The arithmetic operators supported by SQL are listed in the table below:


|Operator | Description |
-------------------------
| +         | Adds two numeric operands |
| -         | Subtracts one numeric operand from another |
| *         | Multiplies two numeric operands |
| /         | Divides one numeric operand by another |
| %         | Calculates the remainder of dividing two numeric operands |


```
SELECT
  3 + 4 as Sum,
  5 - 2 as Diff,
  6 * 8 as Mul,
  10 / 2 as Div,
  8 % 3 as Mod;
```
In the SQL query example above, we use various arithmetic operators to perform arithmetic operations on numeric data. The value of the first column returned is 3 + 4 = 7, the value of the second column returned is 5 - 2 = 3, the value of the third column returned is 6 * 8 = 48, the value of the fourth column returned is 10 / 2 = 5, and the value of the fifth column returned is 8 % 3 = 2.

### Comparison operators


|Operator | Description |
|---------|-------------|
| =       | Equals      |
| !=, <>  | Not equals  |
| >       | Greater than |
| >=      | Greater than or equals |
| <       | Less than |
| <=      | Less than or equals |
| LIKE    | Searches for a specified pattern in a column |
| BETWEEN...AND... | Returns TRUE if a given value falls within a specified range |
| IN               | Returns TRUE if a specified value is present in the list |


Few examples of comparison operators

The `!=` operator is used for checking inequality.

```
SELECT
  *
FROM
  Customer
WHERE
  age != 22; -- Not Equals
```
The statement selects all the rows from the Customer table where the age is not equal to 22
---

The `>` operator is used to check for the “greater than” condition.

```
SELECT
  *
FROM
  Customer
WHERE
  age > 22; -- Greater than
```
This statement selects all the rows from the Customer table where the age is greater than 22.
---

The `>=` operator is used for checking the “greater than or equal to” condition.

```
SELECT
  *
FROM
  Customer
WHERE
  age >= 22; -- Greater than or equal to
```

This statement selects all the rows from the Customer table where the age is greater than or equal to 22.

---

The `<` operator is used to check the “less than” condition.

```
SELECT
  *
FROM
  Customer
WHERE
  age < 22; -- Less than
```

This statement selects all the rows from the Customer table where the age is less 22.

---

The `<=` operator is used to check the “less than or equal to” condition.

```
SELECT
  *
FROM
  Customer
WHERE
  age <= 22; -- Less than or equals
```

This statement selects all the rows from the Customer table where the age is less than or equal to 22.

### The LIKE operator

The LIKE operator is used to search for a specified pattern in a column. The list of various wildcard characters that can be used in combination with the LIKE operator is given below:


|Symbol | Description |
|-------|-------------|
| %     | Matches any number of characters |
| _     | Matches a single character |

```
SELECT
  *
FROM
  Customer
WHERE
  city LIKE '%ton'; -- LIKE
```

This statement selects all the rows from the Customer table where the city’s name ends with the “ton” pattern.

> Tip: The LIKE operator is case-sensitive, To make the search case-insensitive, we can use the "ILIKE" operator instead


### The BETWEEN and AND operator

```
SELECT
  *
FROM
  Customer
WHERE
  age BETWEEN 22 AND 24; -- BETWEEN
```

This statement selects all the rows from the Customer table where the age is between the range of 22 and 24.


### The IN operator

```
SELECT
  *
FROM
  Customer
WHERE
  city IN ('New York', 'Boston', 'Los Angeles'); -- IN
```

This statement selects all the customers from the table who live in either 'New York', 'Boston', or 'Los Angeles'. The IN keyword is used to specify a list of values to compare against. In this case, we compare three different cities. If any of those three cities match what’s in the city column for a particular customer, that customer will be returned.

