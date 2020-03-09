# Database Basics

*Database:* an organized collection of data that can be accessed, managed and updated. Most databases contain several tables that all relate to each other. Databases are useful because:
- They easily support storing large number of records, often in the millions of records, quickly and efficiently.
- They enable central storage of all of a company's data.
- They support a structured query syntax to retrieve, insert, and update data.
- They enforce consistency and integrity of data so data won't get lost or corrupted.

*Relational databases:* sort of like an excel spreadsheet, where each column represents a name and datatype, and each row is the entity. Unlike a spreadsheet, however, although there are columns and rows, they all relate to each other. In our vending machine project:

- Each row is an individual project entity.
- Each column is an attribute of that individual entity (ID, name, date created, etc)

*RDBMS Systems (relational database management systems):* a computer application that manages the definition, storage, retrieval and administration of these databases What we're using is *PostgreSQL.* There is also MS SQL Server, Oracle, DB2, MySQL, PostgreSQL...

## SQL Data Types

*SQL:* structured query language. 

Unlike programming languages, they all use a basic command set; it's standardized, called ANSI (American National Standard Institute).

RDDMS make sure that data going into your DB must match certain types. They do that by specifying the data types in the columns. That way, we know what type of data is going *into* the table, but also *out* of the table. It prevents stuff like a user entering "Frank" as their age and breaking the system.

Here are examples of literals and their data types:
- character string(n), fixed length: '59', 'Python'
- numeric: 10.34, 2.0, .001, -125. 2.5E2
- smallint: no decimals, 5 precision
- largeint: no decimals, 19 precision
- boolean: TRUE, FALSE, UNKNOWN values
- datetime: DATE, '2016', 'dd-MM-yyy'
- varchar(n), variable   lengths: string of characters of *n* length

It's important to note that many SQL databases have a few of their own data types specific to their databases. Postgres, for example, has a *serial* type.

*Serial data type:* postgres's unique data type (doesn't exist elsewhere) that is an auto-incrementing integer used for unique values in a table.

## Functions

With imperative languages, you're giving a computer instructions for everything you want it to do. With SQL languages, you're giving the computer conditions and asking them to retrieve answers. Some of the conditions:

- `==`
- `>`
- `<`
- `>=`
- `<=`
- `!=` or `<>`
- `IN (..., ..., ...)`
- `BETWEEN ... AND ...`
- `IS NULL`
- `IS NOT NULL`
- `LIKE '%a%'` returns anything with an A in it
  - `LIKE '%a'` returns anything that ends with an A
  - `LIKE 'a%'` returns anything that starts with an A

Using SQLs is like asking a question. Given a list of cities, we can ask for all the cities that are like "Phil."

## Basic SQL Structure

#### SELECT

- `SELECT COUNT(*) FROM country;`
  - this is a function called `COUNT`
  - we're just counting the number of rows
- `SELECT * FROM country;`
  - this actually lists everything from `country`
  - the shortcut to run this is CTRL + DOWN
  - `*` this is just a wildcard that lists *all*
-  `SELECT * FROM country LIMIT 10;` let's supposed we just want a *sample* of a data set. they will be in natural order, which is the order in which they are in the system

#### ORDER BY

-  `SELECT * FROM country ORDER BY name LIMIT 10;`
   -  now they are listed alphabetically
-  `SELECT * FROM country ORDER BY gnp DESC LIMIT 1;`
   - lists the country with the highest gnp

#### WHERE

- `SELECT * FROM country WHERE lifeexpectancy IS NOT NULL ORDER BY lifeexpectancy DESC LIMIT 5;`
    - case sensitive!

#### NULL
- `IS NOT NULL` makes sure we're only returning results that have values
- `SELECT lifeexpectancy AS le FROM country WHERE
- 
- 
- `lifeexpectancy IS NOT NULL ORDER BY lifeexpectancy DESC LIMIT 5;`
  - replaces lifeexpectancy with the `le` alias in the actual table view; the tab will say `le` instead of `lifeexpectancy`
  
### AS

- `SELECT c.code, name, c.continent FROM country AS c ORDER BY c.lifeexpectancy DESC;`
  - `c` is just an alias for country
  - `AS` is not necessary
- `SELECT c.code, name, c.continent FROM country c ORDER BY c.name ASC;`
- `SELECT c.code, name, c.continent FROM country c WHERE c. name BETWEEN 'D' and 'G' ORDER BY c. name ASC;`
  - lists all of the countries with names that begin with D-G
- - `SELECT c.code, name, c.continent FROM country c WHERE c. name BETWEEN 'D' and 'France' ORDER BY c. name ASC;`
  - note that the `BETWEEN` keyword is inclusive
- `SELECT c.code, name, c.continent FROM country c WHERE c.name LIST ` `Island%` `ORDER BY c.name ASC:`
  - will search for countries that have `Island` in the name
- `SELECT c.code, c.name, c.continent FROM country c WHERE c.name IN ('Cayman Islands','Turks and Caicos Islands','Falkland Islands') ORDER BY c.name ASC;`
  - this will grab the `code` list, `name` list, and `continent` list and list them in that order from the country data set and list the three countries specified while sorting them in alphabetical order
- `%North%` will return results that contain `North`

Note: the order of the keywords matter:
- from
- where
- order by
- limit

Concatenated names are discouraged. They're hard to read and you can't use pascal case. Best practice: underscore between words.

## Comments In SQL

- `--` will give you a single line comment
- `/*` ... `*/` will give you a block comment

## Examples

#### Name and population of all cities in Ontario, Canada (27 rows)

```
SELECT
    cty.name,
    cty.population // cty is an alias
FROM city cty // you declare aliases here after SELECT
WHERE
    countrycode = 'CAN'
    AND
    district = 'Ontario'
ORDER BY name ASC;`
```

#### Name and population of all cities in Montana (1 row)

```
SELECT
    cty.name,
    cty.population
FROM city cty
WHERE district = 'Montana';
```

#### Name, form of government, and head of state of all countries in Europe (46 rows)

```
SELECT
    c.name,
    c.governmentform,
    c.headofstate  // note again, c is used before
FROM
    country c // we declare it here
WHERE
    c.continent = 'Europe`;
```