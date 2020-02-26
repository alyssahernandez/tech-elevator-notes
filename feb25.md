# Aggregate Functions

## Order of Functions

- `SELECT` : select what type of data you're returning (ex: the `name` column)
- `FROM` : declares which data set you're pulling from
- `WHERE` : defines conditions (ex: `WHERE population = 1000`)
- `GROUP BY`
- `ORDER BY`
- `HAVING`
- `LIMIT`



`HAVING` does not limit on the list, but on the *results*, whereas `WHERE` limits your results.

A `WHERE` clause is used is filter records from a result.  The filter occurs before any groupings are made.
A `HAVING` clause is used to filter values from a group.

## AS Function

In the `FROM` clause, you can say `FROM country AS c` or you can just say `FROM country c`. In the `SELECT` clause, you *could* use an `AS` but don't.

## Aggregate Functions

- `SUM()`
- `COUNT()` : will give us the number of rows
- `AVG()` : gives us the average of 10, 20 and 30, for example

SELECT MIN(price) FROM 

## Sequel Clauses

- `GROUP BY` : groups aggregate functions by attribute


SELECT MIN(price) FROM bookstore b WHERE ORDER BY b.genre 

## Subqueries

Let's say you have the *city* data set. We want to list the cities that have 

-- SUBQUERIES
-- Find the names of cities under a given government leader

        SELECT c.name
        FROM city c
        WHERE c.countrycode IN (SELECT code FROM country WHERE headofstate = 'Elisabeth II');
        -- could also do NOT IN to say every city not under her rule
        -- IN (SELECT ...) pulls data from another data set