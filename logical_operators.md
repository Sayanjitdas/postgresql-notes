## Logical Operators in SQL

Content
---
- [AND](#and-operator)
- [OR](#or-operator)
- [NOT](#not-operator)
- [ANY](#any-operator)
- [ALL](#all-operator)



| Operator | Meaning |
|----------|---------|
| AND      | Returns TRUE if all of the conditions are true |
| OR       | Returns TRUE if one or more of the conditions are true |
| NOT      | Returns TRUE if a condition is false |
| ANY      | Returns TRUE if any of the subquery values meet the condition |
| ALL      | Returns TRUE if all of the subquery values meet the condition |

### AND operator

```
SELECT
  *
FROM
  Customer
WHERE
  gender = 'M'
  AND age > 22; -- AND operator
```
This statement selects all the rows from the Customer table where the customer’s age is greater than 22 and the gender is male.


### OR operator

```
SELECT
  *
FROM
  Customer
WHERE
  gender = 'M'
  OR age > 22; -- OR operator
```
This statement selects all the rows from the Customer table where the customer’s age is greater than 22 or the gender is male.

### NOT operator

```
SELECT
  *
FROM
  Customer
WHERE
  NOT gender = 'M'; -- NOT operator
```

This statement selects all the rows from the Customer table where the gender is NOT equal to 'M'.

### ANY operator

```
SELECT
  <column_1>, <column_2>, ... <column_n>
FROM
  <table_name>
WHERE
  <column_name> { = | > | < } ANY (<value_1>, <value_2>, ... , <value_n>);
```

Example

```
SELECT
  *
FROM
  Customer
WHERE
 gender = 'M'
AND age > ANY ('{22, 23}'); -- ANY operator
```
The `ANY` operator returns `TRUE` if at least one value in the list meets the condition. In this example, the age of male customers must be greater than `22` or `23` to return a `TRUE` result for this expression.

```
SELECT
  *
FROM
  Customer
WHERE
  age < ANY -- ANY Operator
  ( 
    SELECT
      AVG (age)
    FROM
      Customer
  );
```

We can also provide sub queries as well like above.


### ALL operator

```
SELECT
  <column_1>, <column_2>, ... <column_n>
FROM
  <table_name>
WHERE
  <column> { = | > | < } ALL (<value_1>, <value_2>, ... , <column_n>);
```

Example

```
SELECT
  *
FROM
  Customer
WHERE
  gender = 'M'
  AND age > ALL ('{22, 23}'); -- ALL operator

```

The ALL operator returns TRUE if all the values in the list meet the condition. In this example, the male customer’s age must be greater than both 22 and 23 to return a TRUE result for this expression.

