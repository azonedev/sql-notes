 ### What is Database ?
Database is collectation of inter-related of inter-related data, from which we can easily manipulate data.

In a database have multiple entity & in a entity have multiple attributes.

 ### About SQL (intro).

SQL - Structured query language is used to communicate with a database. According to ANSI (American National Standards Institute), it is the standard language for relational database management systems.

 ### Create Database :

    CREATE DATABASE databasename;
#### Create Database with collation:
    CREATE DATABASE db_name 
    CHARACTER SET utf8
    COLLATE utf8mb4_general_ci;
#### Modify Database char & collation:
    ALTER DATABASE db_name
    [DEFAULT] CHARACTER SET charset_name]
    [DEFAULT] COLLATE collation_name]

 ### Delete Database :
    DROP DATABASE database_name;

### Comment In SQL :

    -- Single line Comment define with [--]
<!-- multiline Comment -->
    /* 
        multi-line comment with /*...*/
    */
 ### Create Table :
Syntax:

    Create table table_name(
        colmn_name datatype constrains
    );
<br>
Example:

    Create table users(
        id int not null auto_increment,
        name varchar(100),
        email varchar(50),
        password varchar(100),
        PRIMARY KEY(id)
    );

* [Constraints](#constraints) 
* [Data Types](#about-sql-intro)
* [Primary Key](#primary-key)

 ### Delete Table:
    DROP TABLE table_name

 ### Alter Table: 
The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table.
And  also used to add and drop various constraints on an existing table.

#### Rename Table:
    ALTER TABLE authors 
    RENAME author
#### Rename Column:
    ALTER TABLE table_name 
    change existing_column new_column_name datatype;
<!-- example -->
    ALTER TABLE author 
    change mail email varchar(20);

 #### Add Column:
    ALTER TABLE table_name 
    ADD column_name datatype;
<!-- example -->
    ALTER TABLE users 
    ADD password varchar(100);

 #### Drop Column:
    ALTER TABLE table_name
    DROP column_name;
<!-- example -->
    ALTER TABLE users 
    DROP password;

### Constraints:
SQL constraints (বাদ্ধ্যবাধকতা) are used to specify rules for data in a table.

Available constraints in SQL:
 * NOT NULL - Ensures that a column cannot have a NULL value
 * NULL - a column can have a NULL value
 * UNIQUE  - Ensures that all values in a column are different
 * DEFAULT 
 * PRIMARY KEY
 * FOREIGN KEY
 * CHECK
 * CREATE INDEX

#### Default: 
The `DEFAULT` constraint is used to set a default value for a column.

    column_name datatype DEFAULT value;
    
#### Primary key: 
The `PRIMARY KEY` constraint uniquely identifies each record in a table.
Primary keys must contain UNIQUE values, and cannot contain NULL values.
    
    CREATE TABLE Users (
        id int NOT NULL auto_increment,
        age int,
        PRIMARY KEY (id)
    );
#### Foregin  key: 
A `FOREIGN KEY` is a field (or collection of fields) in one table, that refers to the `PRIMARY KEY` in another table. 

    CREATE TABLE Users (
        id int NOT NULL auto_increment,
        age int,
        role_id int,
        PRIMARY KEY (id),
        FOREGIN KEY (role_id) REFERENCES roles(role_id)
    );

Add Foregin key on existing column of a table :

    ALTER TABLE Orders

    ADD FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID); 

Drop Foregin key form a table :

    ALTER TABLE Orders
    DROP FOREIGN KEY PersonID;

#### Check: 
The `CHECK` constraint is used to limit the value range that can be placed in a column.

    CREATE TABLE Users (
        ID int NOT NULL,
        LastName varchar(255) NOT NULL,
        FirstName varchar(255),
        Age int,
        CHECK (Age>=18)
    );
<!-- add-check -->
    ALTER TABLE users
    ADD CHECK (Age>=18);
<!-- drop check -->
    ALTER TABLE Persons
    DROP CHECK CHK_PersonAge;

#### Create Index:
The `CREATE INDEX` statement is used to create indexes in tables.
`Indexes` are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.

    CREATE INDEX index_name
    ON table_name (col1,col2,...);
<!-- drop index -->
    ALTER TABLE table_name
    DROP INDEX index_name

[more explaination on index...](https://www.youtube.com/watch?v=E--yzX05_k8)


### Select :
`SELECT` QUERY is used to fetch the data from database.

It is the most frequently used SQL command and has the following general syntax:

    SELECT 
    [DISTINCT|ALL ]
    { * | [fieldExpression [AS newName]}
    FROM tableName
    [alias] 
    [WHERE condition]
    [GROUP BY fieldName(s)]  
    [HAVING condition] 
    ORDER BY fieldName(s)

Here, 

`SELECT` is the SQL keyword that lets the database know that you want to retrieve data.

`[DISTINCT | ALL]` are optional keywords that can be used to fine tune the results returned from the SQL `SELECT` statement. If nothing is specified then ALL is assumed as the default.

`{*| [fieldExpression [AS newName]} at least one part must be specified, "*"` selected all the fields from the specified table name, fieldExpression performs some computations on the specified fields such as adding numbers or putting together two string fields into one.

`FROM` tableName is mandatory and must contain at least one table, multiple tables must be separated using commas or joined using the `JOIN` keyword.

`WHERE` condition is optional, it can be used to specify criteria in the result set returned from the query.

`GROUP BY` is used to put together records that have the same field values.

`HAVING` condition is used to specify criteria when working using the `GROUP BY` keyword.

`ORDER BY` is used to specify the sort order of the result set.

#### Select Examples:

    SELECT * FROM users;

    Select specific column data :
    -------------------
    SELECT name,email FROM users;


    Using `AS` Keyword, you can set a customize name on any column when select a data :
    -------------------
    SELECT name AS user_name, email AS user_mail FROM users;

    Concat multiple column data :
    -------------------
    SELECT CONCAT(column1,column2,..) AS new_column FROM table;

    Select distinct : (it returns only different values)
    -------------------
    SELECT DISTINCT name FROM users;

### Where Clause:
`WHERE` Clause in MySQL is a keyword used to specify the exact criteria of data or rows that will be affected by the specified SQL statement. The WHERE clause can be used with SQL statements like INSERT, UPDATE, SELECT, and DELETE to filter records and perform various operations on the data.

Syntax:

    SELECT * FROM tableName WHERE condition;
<!-- example -->
    SELECT * FROM users WHERE age>30;
`NB:` Where clause combined with logical operator[>,<,<>,`AND`, `OR`, `NOT`] & some keyword to implement conditions better way.

#### Where AND:
    where condition1, condition2 both are ture
<!-- example & syntax -->
    SELECT * FROM `users` WHERE `age` >= 18 AND `sex` = 'male';

#### Where OR:
    where condition1, condition2 one or both will be true

<!-- example -->
    SELECT * FROM `users` WHERE `age` >= 18 OR `sex` = 'male';

#### Where In:
* `WHERE IN `returns values that match values in a list.
* This list is hardcoded or generated by a [subquery](#subquery).
* WHERE IN is shorthand for multiple OR conditions.
  
example :

    SELECT * FROM film WHERE length IN(50, 55)

sub-query:

    SELECT *
    FROM language
    WHERE language_id IN 
        (SELECT language_id FROM film )

`*NB`: if you want to select items that don't exist on the array/list, then you have to use `NOT IN ` alter of `IN`

### INSERT INTO:
'INSERT INTO 'is used to store data in the tables.

Basic Syntax:

    INSERT INTO tableName (col1, col2, col3, ...) VALUES (data1, data2, data3, ...);

Example :
    
    INSERT INTO members (full_names,gender,physical_address,contact_number) 
    VALUES ('Sheldon Cooper','Male','Woodcrest', '0976736763');



`NB:` Changing the order of the columns has no effect on the INSERT query in MySQL as long as the correct values have been mapped to the correct columns.

#### Inserting into a Table from another Table:

The INSERT command can also be used to insert data into a table from another table. The basic syntax is as shown below.

    INSERT INTO table_1 SELECT * FROM table_2;   

example:

    INSERT INTO categories_archive 
    SELECT * FROM categories;

speacific :

    INSERT INTO categories_archive(category_id,category_name,remarks) 
    SELECT category_id,category_name,remarks FROM categories;

### DELETE:
Delete command is used to delete rows that are no longer required from the database tables

Syntax :

    DELETE FROM table_name [WHERE condition];

Example :

    DELETE FROM users WHERE user_id = 1;

### UPDATE :
The `UPDATE` command can be used to update a single field or multiple fields at the same time. It can also be used to update a MySQL table with values from another table.

syntax:

    UPDATE tablename 
    SET col1 = val1, col2 = val2,...
    WHERE condition;

Example :

    UPDATE books
    SET name = 'Signature Mind', author_id = 1
    WHERE id = 2;

### ORDER BY [ Data Sorting ]:
`ORDER BY` clause is used to sort the data in ascending or descending order, based on one or more columns. Some databases sort the query results in an ascending order by default.

Syntax :

    SELECT statement... 
    [WHERE condition | GROUP BY field_name(s) HAVING condition]
    ORDER BY field_name(s) [ASC | DESC];
* [Select](#select) is the regular select query
" | " represents alternatives
* [ [Where](#where-clause)" condition | [Group By](#group-by) `field_name(s)` [Having](#having) condition" is the optional condition used to filter the query result sets.
* `ORDER BY` performs the query result set sorting
* `[ASC | DESC]` is the keyword used to sort result sets in either ascending or descending order. Note `ASC` is used as the default.

#### Order by column :

    SELECT * FROM movies 
    ORDER BY country_id;

    SELECT * FROM movies 
    ORDER BY country_id, release_year;

#### Order by ascending & descending order:

    SELECT * FROM movies
    ORDER BY country_id DESC;

    SELECT * FROM movies 
    ORDER BY country_id ASC, release_year DESC;

    *ASC use for ascending order

### LIMIT :

The `limit` keyword is used to limit the number of rows returned in a query result.

Syntax:
    
    SELECT * FROM tablename
    ...
    LIMIT numberOfRows;

Example: 

    SELECT * FROM movies
    WHERE language = 'en'
    ORDER BY country_id DESC
    LIMIT 5;


### OFFSET:
If you want the query to return entries starting from a particular line, you can use `OFFSET` clause to tell it where it should start. And the practrial example will be pagination.

Syntax :

    SELECT * FROM tableName ...
    LIMIT (n)
    OFFSET (n)number

    SELECT * FROM movie
    WHERE category="action"
    LIMIT 25
    OFFEST 30;

Limit with offset :

    SELECT * FROM tableName ...
    LIMIT numberOfOffest, numberOfLimit;

    SELECT * FROM movie
    WHERE language = "en"
    LIMIT 30, 25;



### Learning Resources:

* W3Schools
* Guru99
* [DBMS By Gate Smashers --tutorial_hindi](https://www.youtube.com/playlist?list=PLxCzCOWd7aiFAN6I8CuViBuCdJgiOkT2Y)
* geekforgeeks
* [Sololearn](https://www.sololearn.com/learning/1060)