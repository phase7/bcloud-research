# bcloud-research
This repo is about the research project launched  by Brilliant Cloud Technologies.

# Postgresql
<p align="center"><a href="https://www.postgresql.org/">
<img align="center" src="https://raw.githubusercontent.com/solaimanhridoy/LearnPostgreSQl/master/img/postgresql-card.png">
</a></p>

At first we are getting hands dirty with postgresql on local machine.

## Installation
Check out my [postgres installation overview](https://github.com/phase7/bcloud-research/blob/phase7-install-postgres/install-postgres-manjaro.md) to see how I installed on Manjaro.

## Postgres Shell
We can get into the shell by executing psql command. We will likely see our default user name. in this shell we can run the following commands to inspect database and execute  tasks. Below we will look at some of the most useful commands of postgres command line tool. (will update as I go on)

| Commands  | What they do                                                |
|-----------|-------------------------------------------------------------|
| \q        | quit psql                                                   |
| \i FILE   | execute commands from file                                  |
| \d        | list tables, views, and sequences                           |
| \d TABLENAME| Show table schema and other details of `TABLENAME` table                                  |
| \l        | list databases                                              |
| \c DBNAME | connect to new database DBNAME (currently default username) |
| \x        | Expand view; To see long table records in a beautiful manner|
| \df        | View available functions; like uuid generation.|

## Basic SQL (common operations and keywords)

Following are some basic sql commands for beginners. (will update as I go on)

| Operation                                    | Query                                                                                                                                                                                                                | What you should know about them                                                                                             |
|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Create your database    | CREATE DATABASE dbname;                                                                                                                                                                                              | create a database named DBNAME                                                                                              |
| Delete your DB                             | DROP DATABASE dbname;                                                                                                                                                                                              | Delete a database named DBNAME                                                                                              |
| Create a table                               | CREATE TABLE person (   id BIGSERIAL NOT NULL PRIMARY KEY,   first_name VARCHAR(50) NOT NULL,   last_name VARCHAR(50) NOT NULL,   gender VARCHAR(8) NOT NULL,   email VARCHAR(150),   date_of_birth DATE NOT NULL ); | Create a new table schema with constarints                                                                                  |
| Delete a table                               | DROP TABLE tablename                                                                                                                                                                                                 | Delete a table. In db this is colloquilly called dropping a table.                                                          |
| Insert new value in table                    | INSERT INTO tablename (   col_name ) VALUES ('value');                                                                                                                                                               | insert `value` in the `col_name` column of `tablename` table                                                                |
| Insert multiple values                       | INSERT INTO person (   first_name,   last_name,   gender,   date_of_birth ) VALUES ('hey', 'bro', 'male', DATE '1234-5-6');                                                                                          | insert multiple values at multiple columns at once.                                                                         |
| Show all rows of a table                     | SELECT * FROM tablename;                                                                                                                                                                                             | all data from a table - `tablename`                                                                                         |
| Show specific rows                           | SELECT col1, col2 FROM tablename;                                                                                                                                                                                    | chosen column data from a table - `tablename`                                                                               |
| Sort data and show them                      | SELECT * FROM tablename ORDER BY col_name [ASC/DESC]                                                                                                                                                                 | show data in a sorted manner, either ASCending, or DESCending order                                                         |
| Get distinct data                            | SELECT DISTINCT col_name FROM tablename;                                                                                                                                                                             | Show unique data, rejecting the duplicate ones                                                                              |
| Filter data based on condition               | SELECT * FROM tablename WHERE col='value';                                                                                                                                                                           | Show filtered data when conditions such as specific value for a column is matched!                                          |
| Filter data based on more than one condition | SELECT  *  FROM  tablename  WHERE  col1< 'value1'   AND  (col2>= 'value2'   OR  col3<> 'value3' );                                                                                                                   | Multiple conditions can be made with `AND` and `OR` operators. (`<>` is the `!=` for SQL)                                   |
| Skip rows and get specific number of rows    | SELECT * FROM tablename OFFSET 5 LIMIT 5;                                                                                                                                                                            | To get row from 6 to 10. (While `OFFSET` is ANSI Standard, `LIMIT` is limited (_pun intended_) to `postgresql` and `mysql`) |
| Same as above, but universal                 | SELECT * FROM tablename OFFSET 5 FETCH FIRST 5 ROW ONLY;                                                                                                                                                             | To get row from 6 to 10 following ANSI all the way. `FETCH` is present in all DB Engines.                                   |
| Set data range                       | SELECT * FROM tablename WHERE col_name BETWEEN 'value1' AND 'value2';                        | get data output between given ranges                                                                     |
| Check condition for particular cases | SELECT   *   FROM  tablename  WHERE  col_name  IN  ( ' value1 ' , ' value2 ' ,  ' value3 '); | check for selected conditions. this method can be helpful to get multiple  or conditions checked easily. |

## Intermediate SQL (Operators and operations)

| Operation                              | Query                                                                                                                                                                           | What you should know about them                                                                                                                                                                                                      |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Condition matching using patterns      |  - SELECT * FROM tablename WHERE col_name LIKE 'pattern'; - SELECT * FROM person WHERE email LIKE '%gmail%';                                                                    | select only conditions that matches pattern. For example, the second query will select all emails that have gmail in them. For details in pattern matching [click here](https://www.postgresql.org/docs/9.3/functions-matching.html) |
| Delete a specific row                  | DELETE FROM tablename WHERE col_name='value';                                                                                                                                   | delete the condition matching row                                                                                                                                                                                                    |
| Update a value on a specific condition | UPDATE tablename SET col_name='new_value' WHERE id='something';                                                                                                                 | you can use all conditions allowed for SELECT operation to update a value                                                                                                                                                            |
| Add primary key                        | ALTER TABLE tablename ADD PRIMARY KEY (col_name);                                                                                                                               | Add a column as the primary key.[Details here](https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-PRIMARY-KEYS)                                                                                            |
| Create a constraint                    | ALTER   TABLE  person ADD  CONSTRAINT unique_email UNIQUE(email)                                                                                                                | Add a constraint for a column, here the value must be `UNIQUE`                                                                                                                                                                       |
| Create a condition constraint          | ALTER TABLE person ADD CONSTRAINT gender_constraint CHECK(gender = 'Male' OR gender = 'Female');                                                                                | Add a constraint for selective conditions to be met.                                                                                                                                                                                 |
| Remove a constraint                    | ALTER TABLE person DROP CONSTRAINT constraint_name                                                                                                                              | Remove a constraint that is already set on column.[Check for details on constraints here](https://www.postgresql.org/docs/9.4/ddl-constraints.html)                                                                                  |
| Ignore exceptions                      | INSERT into tablename (col_name) VALUES ('values') ON CONFLICT (unique_col) DO NOTHING;                                                                                         | If an constraint is not maintained in a new insert query, you can skip it.                                                                                                                                                           |
| Handle exceptions                      | INSERT into tablename (col_name) VALUES ('values') ON CONFLICT (unique_col) DO UPDATE SET col_name=EXCLUDED.col_name;                                                           | You can handle the exception and take proper actions to resolve the issue.Here the `EXCLUDED` refers to the new entry's values.                                                                                                      |
| Add foreign key                        | CREATE TABLE person (id BIGSERIAL NOT NULL PRIMARY KEY,first_name VARCHAR(50) NOT NULL,last_name VARCHAR(50) NOT NULL,car_id BIGINT REFERENCES car (id),UNIQUE (car_id) );      | Add a foreign key column using `REFERENCE` keyword                                                                                                                                                                                   |

## Aggregate Funtions
Here are the ageneral aggregate functions available for postgres.

|              Function              |                                 Argument Type(s)                                |                                                             Return Type                                                             | Partial Mode |                                                               Description                                                              |
|:----------------------------------:|:-------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------:|:------------:|:--------------------------------------------------------------------------------------------------------------------------------------:|
|  array_agg(expression)             | any non-array type                                                              | array of the argument type                                                                                                          | No           | input values, including nulls, concatenated into an array                                                                              |
| array_agg(expression)              | any array type                                                                  | same as argument data type                                                                                                          | No           | input arrays concatenated into array of one higher  dimension (inputs must all have same dimensionality, and cannot be empty  or null) |
|   avg(expression)                  | smallint, int, bigint, real, double precision, numeric, or interval             | numeric for any integer-type argument, double precision for a floating-point argument, otherwise the same as the argument data type | Yes          | the average (arithmetic mean) of all non-null input values                                                                             |
|  bit_and(expression)               | smallint, int, bigint, or bit                                                   | same as argument data type                                                                                                          | Yes          | the bitwise AND of all non-null input values, or null if none                                                                          |
|  bit_or(expression)                | smallint, int, bigint, or bit                                                   | same as argument data type                                                                                                          | Yes          | the bitwise OR of all non-null input values, or null if none                                                                           |
|  bool_and(expression)              | bool                                                                            | bool                                                                                                                                | Yes          | true if all input values are true, otherwise false                                                                                     |
|  bool_or(expression)               | bool                                                                            | bool                                                                                                                                | Yes          | true if at least one input value is true, otherwise false                                                                              |
|  count(*)                          |                                                                                 | bigint                                                                                                                              | Yes          | number of input rows                                                                                                                   |
| count(expression)                  | any                                                                             | bigint                                                                                                                              | Yes          | number of input rows for which the value of expression is not null                                                                     |
|  every(expression)                 | bool                                                                            | bool                                                                                                                                | Yes          | equivalent to bool_and                                                                                                                 |
|  json_agg(expression)              | any                                                                             | json                                                                                                                                | No           | aggregates values, including nulls, as a JSON array                                                                                    |
|  jsonb_agg(expression)             | any                                                                             | jsonb                                                                                                                               | No           | aggregates values, including nulls, as a JSON array                                                                                    |
|  json_object_agg(name, value)      | (any, any)                                                                      | json                                                                                                                                | No           | aggregates name/value pairs as a JSON object; values can be null, but not names                                                        |
|  jsonb_object_agg(name, value)     | (any, any)                                                                      | jsonb                                                                                                                               | No           | aggregates name/value pairs as a JSON object; values can be null, but not names                                                        |
|  max(expression)                   | any numeric, string, date/time, network, or enum type, or arrays of these types | same as argument type                                                                                                               | Yes          | maximum value of expression across all non-null input values                                                                           |
|  min(expression)                   | any numeric, string, date/time, network, or enum type, or arrays of these types | same as argument type                                                                                                               | Yes          | minimum value of expression across all non-null input values                                                                           |
|  string_agg(expression, delimiter) | (text, text) or (bytea, bytea)                                                  | same as argument types                                                                                                              | No           | non-null input values concatenated into a string, separated by delimiter                                                               |
|  sum(expression)                   | smallint, int, bigint, real, double precision, numeric, interval, or money      | bigint for smallint or int arguments, numeric for bigint arguments, otherwise the same as the argument data type                    | Yes          | sum of expression across all non-null input values                                                                                     |
|  xmlagg(expression)                | xml                                                                             | xml                                                                                                                                 | No           | concatenation of non-null XML values (see also Section 9.14.1.7)                                                                       |

For more functions that are useful for staistics and such, follow [this link](https://www.postgresql.org/docs/current/functions-aggregate.html).

## Join operations
![sql-join-w3school]

| Operation                                            | Query                                                  | What you should know about them                                                              |
|------------------------------------------------------|--------------------------------------------------------|----------------------------------------------------------------------------------------------|
| Inner join, get the common result                    | `SELECT * FROM person JOIN car ON person.car_id=car.id;` | merge two tables based on the condition and get only the common result(s)                  |
| Left join, get the common plus all of the left table | SELECT * FROM person LEFT JOIN car using(car_uid)      | In this join you'll get all inner join results with the complete left table you have joined. |

[Different `join` operations from postgres official doc](https://www.postgresql.org/docs/12/queries-table-expressions.html#QUERIES-FROM)

## Date and Time  on Postgres
For date and time operations, the `NOW()` function is widely used. Examples given below.

```sql
SELECT NOW();         # 2020-08-13 21:16:10.665998+06
SELECT NOW()::DATE;   # 2020-08-13
SELECT NOW()::TIME;   # 21:17:09.700756
```
We can process this data further.

| Operation                          | Function                                                                                                | Output                                |
|------------------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------|
| Subtract specific time from now    | SELECT NOW() - INTERVAL '2 YEAR 1 MONTH';                                                               | 2018-07-13 22:14:21.165973+06         |
| Add specific time to now           | SELECT (NOW() - INTERVAL '2 YEAR 1 MONTH')::DATE;                                                       | 2018-07-13                            |
| Get specific field using `EXTRACT` | SELECT EXTRACT(YEAR from NOW()); SELECT EXTRACT(MONTH from NOW()); SELECT EXTRACT(CENTURY from NOW());  | 2020 8 21                             |
| Calculate age                      | SELECT AGE(NOW(), DATE '2007-7-7') AS age;                                                              | 13 years 1 mon 6 days 22:18:32.906531 |

## Export Query Results to a CSV File

We can take the output of a query and save it as a CSV file. We'll use the following command.

```sql
\copy (SELECT * FROM tablename) TO '/path/to/csv' DELIMITER ',' CSV HEADER;
```

By changing the delimiter we can produce tsv as well.

## Extensions

Extensions can add additional functionalities. We can use `uuid`s by using an extension.

```sql
select * from pg_available_extensions where name like '%uuid%';
```
We get `uuid-ossp`.


We can check all of the extensions available in PostgreSQL by using:

```sql
SELECT * FROM pg_available_extensions;
```

To install an extension:

```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```
We have to run it as the superuser. Otherwise we will face errors. So I have changed my role as superuser.
```sql
ALTER USER <your-user-name> WITH SUPERUSER;
```

Now we can see available functions by writing `\df`.

[sql-join-w3school]: https://github.com/phase7/bcloud-research/blob/master/assets/sql-join-w3school_20200814_113424.png "sql-join-w3school"
