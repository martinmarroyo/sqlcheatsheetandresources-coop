# SQL Cheat Sheet & Practice Resources
## Table of Contents <a name="top"></a>
- #### [Basic Syntax](#basic-syntax) 
- #### [Order of Clauses](#clause-order)
- #### [Operators](#operator)
- #### [Working with Aggregate Functions](#aggregates)
- #### [Joins and multiple tables](#joins)
- #### [Basic Pattern Matching](#patterns)
- #### [Resources - More Practice!](#resources)



## Basic Syntax <a name="basic-syntax"></a> 

**Ex 1:**
``` SQL
SELECT *
FROM table;
```
**Ex 2:**
``` SQL
SELECT column1, column2
FROM table;
```
**Ex 3:**
``` SQL 
SELECT DISTINCT column1, column2
FROM table
WHERE condition1 = some_other_condition;
```
**Ex 4:**
``` SQL
SELECT column1, column2
FROM table
WHERE column1 = some_condition
ORDER BY column1 ASC, column2 DESC
LIMIT 5
OFFSET 5;
```
[back to top](#top)
## Order of Clauses (for a basic query) <a name="clause-order"></a>

This is the general order of clauses for most basic SQL queries. Please note that there are other advanced clauses which are not covered here.
1. `SELECT`
2. `FROM`
3. `JOIN`*
4. `WHERE`*
5. `GROUP BY`*
6. `HAVING`*
7. `ORDER BY`*
8. `LIMIT`*
9. `OFFSET`*

\* *Denotes a clause that is not always required in a query.*

[back to top](#top)

## Operators <a name="operator"></a>

#### Comparison Operators
- **Equal to**: `=`
- **Not equal to**: `<>` or `!=`
- **Greater than**: `>`
- **Less than**: `<`
- **Greater than or equal to**: `>=`
- **Less than or equal to**:  `<=`
- **Match zero to many characters (for `LIKE` clause):** `%`
- **Match any single character (for `LIKE` clause):** `_`

#### Logical Operators
- `AND` - Checks that two or more conditions are ALL true (e.g. `condition1 AND condition2`)
- `OR` - Checks if any of two or more conditions are true (e.g. `condition1 OR condition2`)
- `NOT` - Negates the logical operation that it is placed in front of (e.g. `NOT AND`)
- `IS NULL` - Checks if a value is NULL (meaning there is no data - e.g. `column1 IS NULL`)
- `LIKE` - Matches on similar rather than exact values (e.g. `column1 LIKE 'COOP%'`)
- `BETWEEN` - Checks for values in a range (e.g. `column1 BETWEEN 1 AND 5` checks for a value between 1 and 5 in `column1`)
- `IN` - Checks if a value is in a given set of values (e.g. `column1 IN (1,2,4,5)` checks if any of the values in `column1` are either 1, 2, 4 or 5)

#### Arithmetic Operators
- `+` - Adds two values
- `-` - Subtracts two values
- `*` - Multiplies two values
- `/` - Divides two values

[back to top](#top)

## Working with Aggregate Functions <a name="aggregates"></a>
#### Clauses to know:
- `GROUP BY` - Allows you to aggregate data in by a single value or group of values.
- `HAVING` - Allows you to filter your query using the value of an aggregate function. Think of this as a `WHERE` clause for aggregate functions.
#### Common aggregate functions:
- `COUNT(column)`: Counts how many rows are in a particular column (or table if you use '*' - e.g. `COUNT(*)`).
- `MIN(column)`: Gives you the smallest value found for the given column.
- `MAX(column)`: Gives you the largest value found for the given column.
- `AVG(column)`: Gives you the average for all values in the given column.
- `SUM(column)`: Gives you the sum of all the values in the given column.

**Code examples**

*Finding the total number of rows in a table*
```SQL
SELECT COUNT(*)
FROM table;
```

*Finding the total count of items in a particular column*
```SQL
SELECT COUNT(column1)
FROM table;
```
*Finding the average of values in a column*
```SQL
SELECT AVG(column)
FROM table;
```

*Finding the max value of a column*
```SQL
SELECT MAX(column)
FROM table;
```

*Finding the min value of a column*
```SQL
SELECT MIN(column)
FROM table;
```

*Aggregating by a value using `GROUP BY`*
```SQL
SELECT 
    column1
    ,AVG(column2)
FROM
    table
GROUP BY
    column1;
```
*Aggregating by multiple values using `GROUP BY`*
```SQL
SELECT
    column1
    ,column2
    ,COUNT(column3)
FROM
    table
GROUP BY
    column1
    ,column2;
```
*Using the `HAVING` clause with `GROUP BY`*
```SQL
SELECT
    column1
    ,column2
    ,COUNT(column3)
FROM
    table
GROUP BY
    column1
    ,column2
HAVING COUNT(column3) > 1;
```

[back to top](#top)

## Joins and multiple tables <a name="joins"></a>
#### Types of Joins & Code examples

**`INNER JOIN`**

![Inner Join](https://www.codeproject.com/KB/database/Visual_SQL_Joins/INNER_JOIN.png)

**Ex:**
```SQL
SELECT
    A.column1,
    B.column1
FROM A
INNER JOIN B
ON A.column1=B.column1
```
**`LEFT JOIN`**

![left Join](https://www.codeproject.com/KB/database/Visual_SQL_Joins/LEFT_JOIN.png)

**Ex:**
```SQL
SELECT
    A.column1,
    B.column1
FROM A
LEFT JOIN B
ON A.column1=B.column1
```

**`RIGHT JOIN`**

![right Join](https://www.codeproject.com/KB/database/Visual_SQL_Joins/RIGHT_JOIN.png)

**Ex:**
```SQL
SELECT
    A.column1,
    B.column1
FROM A
RIGHT JOIN B
ON A.column1=B.column1
```

**`FULL OUTER JOIN`**

![outer Join](https://www.codeproject.com/KB/database/Visual_SQL_Joins/FULL_OUTER_JOIN.png)

**Ex:**
```SQL
SELECT
    A.column1,
    B.column1
FROM A
FULL OUTER JOIN B
ON A.column1=B.column1
```
#### Syntax
We typically use dot (`.`) notation when we join two or more tables in SQL. This is so that we don't confuse the SQL engine when two tables have columns with the same name. Here's the syntax:
`table_name.column_name`
**Ex:**
```SQL
SELECT
    A.column1,
    B.column1
FROM A
INNER JOIN B
ON A.column1=B.column1
WHERE A.column1 LIKE 'COOP%'
```
Another thing to keep in mind is that `JOIN` and `INNER JOIN` are the same thing in SQL. Clauses that are effectively the same but written differently are called synonyms. However, while `JOIN` and `INNER JOIN` do the same thing, we tend to prefer the more explicit `INNER JOIN` syntax. This makes your code more clear and easier to understand, which is important when you're working on a team!
[back to top](#top)
## Basic Pattern Matching <a name="patterns"></a>
#### `LIKE` with the `%` Operator
The `%` is known as a wildcard operator. This means that it can be used to match zero (think blank spaces) to many characters in a given string. Here are some examples of how we can use it to filter for text patterns in our data. 
>*The following code:*
>```SQL
> SELECT *
> FROM table
> WHERE column LIKE 'COOP%';
>```
>*will filter for and match any strings that are like the following:*
>- "COOP"
>- "COOP Careers"
>- "COOP Careers: Overcoming Underemployment"

Essentially, this filters for any text string that starts with the word *"COOP"*. We can also use the `%` operator to filter for words within a given text string.
> *The following code:*
>```SQL
>SELECT *
>FROM table
>WHERE column LIKE '%COOP%';
>```
> *will filter for and match any strings that are like the following:*
>- "COOP Careers"
>- "COOP"
>- "It's pronounced **'COOP'** not *'COOP'*"

#### `LIKE` with the `_` Operator
The `_` operator is also a wildcard operator, just like `%`. The only difference is that `_` only matches any single character.
>*The following code:*
>```SQL
> SELECT *
> FROM table
> WHERE column LIKE 'COOP_';
>```
>*will filter for and match any strings that are like the following:*
>- "COOP"
>- "COOP "
>- "COOP1"
> 
>*but it will not match strings like "COOP12"* or "COOP12345*".

[back to top](#top)

## Resources - More Practice! <a name="resources"></a>
- [SQL Bolt](https://sqlbolt.com/): The lessons here are a great introduction to SQL and you know the platform already!
- [Mode](https://mode.com/sql-tutorial/): A comprehensive SQL tutorial from beginner all the way to advanced SQL. There's even a data analytics with SQL tutorial. This is a great resource to learn about SQL in depth and practice what you learn in their online database.
- [StrataScratch](https://platform.stratascratch.com/coding): Practice coding questions geared toward data analysts and data scientists. You can solve coding problems used by real companies for technical interviews using PostgresSQL, Python, R, or MySQL. It's free to sign up!
- [Codecademy - Free Learn SQL Course](https://www.codecademy.com/learn/learn-sql): Codecademy is another great resource to learn SQL as well as most other languages. There are a lot of free resources here that can help you learn SQL, Python, R, and many other languages.
- [Socratica SQL (YouTube)](https://www.youtube.com/watch?v=nWyyDHhTxYU&list=PLih4ch-U2DiBbMoFK4ML9faT3k3MM2UQY): This is a great playlist that will get you started learning SQL with one of the most popular relational databases - Postgres.
- [DB Fiddle](https://dbfiddle.uk/): This site is like a SQL scratch pad. You can use it to practice doing stuff like creating tables and inserting data into them, and all sorts of other stuff that you might not be able to do so freely in a live database. It's a sandbox, basically. Here are a couple of links to fiddles with some data in them to play with: [fiddle 1](https://dbfiddle.uk/?rdbms=postgres_13&fiddle=366b683701596d3f7459b0411c15acd1) and [fiddle 2](https://dbfiddle.uk/?rdbms=postgres_13&fiddle=dfffc1939f629d9286c55d732fb656c5). 
- [Kaggle](https://www.kaggle.com/): Kaggle is the place for data analysis and data science. There are tons of free data sets to try out and even some good, free courses on SQL and Python. 

[back to top](#top)
