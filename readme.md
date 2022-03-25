# How to run MySQL in commands prompt?
```js
mysql -u root -p
```

NOTE: Import SQL file into your database:
```js
USE db_name;
\. <file_path>
```

Show Databases:
```js
show databases;
```

Create Database:
```js
create database vikings;
```

Work on a database:
```js
use vikings;
```

Show Tables:
```js
show tables;
```

Create Table:
```js
create table students (
    -> name varchar(255),
    -> email varchar(100),
    -> mobile varchar(15)
    -> );
```

Table Information:
```js
describe students;
```
Delete Table:
```js
DROP TABLE students;
```

Reset Table Data:
```js
TRUNCATE TABLE students;
```

Create Data:
```js
INSERT into students( name, email, mobile)
    -> VALUES ("Satya","a@com", "123");
```
```js
INSERT into students( name, email, mobile)
    -> VALUES ("B","b@com","124"),
    -> ("C","c@com","125");
```

Show the table Data: or Read Data:
```js
 select * from students;
```
```js
 select name from students;
 select name,email from students;
 select name from students where email = "a@com";
```

Update table Data:
```js
update students  SET name = "B" where email = "124";
update students  SET name = "C" where email = "125";
update students  SET email = "c@com" where email = "125";
update students  SET email = "b@com" where email = "124";
update students  SET mobile = "124" where email = "b@com";
update students  SET mobile = "125" where email = "c@com";
select * from students;

update students set name = "ABC";
// it will affect all the data of name because you missed the where clause
```

Delete Data:
```js
delete from students;
// it will delete all data

delete from students where email = "a@com";
select * from students;
```

**Data Types:**

int - A standard integer
char - A fixed-length string
varchar - A variable-length string
date - A date value in YYYY-MM-DD format
time - A time value in hh:mm:ss format
datetime - A date and time value in YYYY-MM-DD hh:mm:ss format

use database masai:
```js
use masai;
```

use table user_data:
```js
describe user_data;
```

show data:
```js
select * from user_data where gender != "Female";

select * from user_data where gender != "Female" and language = "Lao";

select * from user_data where gender != "Female" and language = "Lao" and shirt_size = "2XL";

select * from user_data where gender != "Female" or language = "Lao";

select * from user_data where language = "Somali" or language = "Lao";

select * from user_data where language in ("Somali", "Lao");

select * from user_data where gender in ("Male") and language in ("Somali", "Lao");

select count(*) from user_data where language in ("Somali", "Lao");

```

use table students_marks:
```js
select * from students_marks where maths > 50;

select * from students_marks where maths < 50;

select * from students_marks where maths between 50 and 60;

select count(*) from students_marks where maths between 50 and 60;

select sum(maths) from students_marks;

select avg(maths) from students_marks;

select avg(maths) from students_marks where gender = "Female";

select avg(maths) from students_marks where gender = "Female" and section = "C";
```

use table cars_data:
```js
select * from cars_data;

describe cars_data;

select distinct(country) from cars_data;

select count(distinct(country)) from cars_data;
```

use the table user_data:
```js
select * from user_data where name like "a%";
// all name start with a;

select * from user_data where name like "%a";
// all the name end with a;

select * from user_data where name like "%ere%";
// all the name contains ere;

select * from user_data where name like "_a%";
// second char is a;

select * from user_data where name like "__a%";
// third char is a;

select * from user_data where name like "%a_";
// second last char is a;

select * from user_data where name like "%a__";
// third last char is a;
```


use table students_marks:
```js
describe students_marks;

select name, (maths+science+english) as total from students_marks;

select name, (maths+science+english)/3 as avg from students_marks;

select min(maths) from students_marks;

select * from students_marks where maths in (select min(maths) from students_marks);

select * from students_marks;

select * from students_marks order by maths asc;

select * from students_marks order by maths asc, science asc;

select * from students_marks order by maths asc limit 10;
select * from students_marks order by maths asc limit 30;

select * from students_marks order by maths asc limit 30, 10;
// first is offset and limit: like 30 is offset and 10 is limit

// Aggregate the query by group by
select count(*), class from students_marks group by class;

select count(*), class, section from students_marks group by class, section;

select count(*), class, section from students_marks group by class, section order by class, section;

select MAX(maths), class, section from students_marks group by class, section order by class, section;

select AVG(maths), gender, class, section from students_marks group by class, section ,gender order by class, section, gender;

select AVG(maths), class, section from students_marks where gender = "Female" group by class, section order by class, section;
// this will not work with aggregation but show the output except where clause;

select AVG(maths) as avg_maths, class, section from students_marks where gender = "Female" group by class, section having avg_maths > 50;

select AVG(maths) as avg_maths, class, section from students_marks where gender = "Female" group by class, section having avg_maths > 50 order by avg_maths desc;
```



# WHERE CLAUSE
```js
/** Get all the users **/
SELECT * FROM user_data;

/** Get all the users where gender is Male **/
SELECT * FROM user_data WHERE gender = "Male";

/** Get all the users where gender is not Male **/
SELECT * FROM user_data WHERE NOT gender = "Male";
SELECT * FROM user_data WHERE gender != "Male";

/** Get all the users where gender is Male and language is Hindi **/
SELECT * FROM user_data WHERE gender = "Male" and language = "Hindi";

/** Get all the users where gender is Male and language is not Hindi **/
SELECT * FROM user_data WHERE gender = "Male" and NOT language = "Hindi";
SELECT * FROM user_data WHERE gender = "Male" and language != "Hindi";

/** Get all the users where shirt size is L or XL **/
SELECT * FROM user_data WHERE shirt_size = "L" or shirt_size = "XL";
SELECT * FROM user_data WHERE shirt_size IN ("L", "XL");

/** Combining multiple conditions **/
SELECT * FROM user_data WHERE (gender = "Male" and shirt_size = 'L') OR (gender = "Female" and shirt_size = 'M');
SELECT * FROM user_data WHERE ((gender = "Male" and shirt_size = 'L') OR (gender = "Female" and shirt_size = 'M')) AND language = "English";
SELECT * FROM user_data WHERE ((gender = "Male" and shirt_size = 'L') OR (gender = "Female" and shirt_size = 'M')) AND language IN ("English", "Hindi");
```

# WHERE OPERATORS
```js
SELECT * FROM students_marks WHERE maths > 50;
SELECT * FROM students_marks WHERE science >= 75;
SELECT * FROM students_marks WHERE english < 40;
SELECT * FROM students_marks WHERE maths <= 50;
/** Both the starting and ending values are included **/
SELECT * FROM students_marks WHERE maths BETWEEN 50 AND 75;
```

# COUNT FUNCTION
```js
SELECT COUNT(id) FROM students_marks WHERE gender = 'Male';
SELECT COUNT(id) FROM students_marks WHERE maths >= 75;
```

# ORDERING RESULTS
```js
SELECT * FROM students_marks WHERE gender = 'Male' ORDER BY maths ASC;
SELECT * FROM students_marks WHERE gender = 'Female' ORDER BY science DESC;
SELECT * FROM students_marks ORDER BY maths ASC, science DESC;
```

# LIMIT & OFFSET
```js
SELECT * FROM students_marks LIMIT 10;
/** The first value is offset (skip) count the second value is limit count **/
SELECT * FROM students_marks LIMIT 20,10;
```

# SUM FUNCTION
```js
SELECT SUM(maths) FROM students_marks WHERE gender = 'Male';
SELECT SUM(maths) FROM students_marks WHERE maths >= 75;
```

# AVG FUNCTION
```js
SELECT AVG(maths) FROM students_marks WHERE gender = 'Male';
SELECT AVG(maths) FROM students_marks WHERE maths >= 75;
```

# LIKE

% and _

% - Any number or characters

_ - Single character

```js
SELECT * FROM students_marks WHERE name LIKE 'a%';
SELECT * FROM students_marks WHERE name LIKE '%a';
SELECT * FROM students_marks WHERE name LIKE '_a%';
SELECT * FROM students_marks WHERE name LIKE '%a_';
SELECT * FROM students_marks WHERE name LIKE '___a%';
```

# DISTINCT
```js
SELECT DISTINCT company FROM employee_salary;
SELECT DISTINCT company, departmement FROM employee_salary;
SELECT COUNT(DISTINCT company) FROM employee_salary;
```

# SUM & AVG
```js
SELECT AVG(maths) FROM students_marks;
SELECT AVG(maths), AVG(science) FROM students_marks;
SELECT SUM(salary) FROM employee_salary;
```

# OPERATIONS

+,-,*,/,%

```js
SELECT (maths+science+english) AS total_marks FROM students_marks;
SELECT (maths+science+english)/3 AS avg_marks FROM students_marks;
```

# Min & Max
```js
SELECT MIN(maths) FROM students_marks;
SELECT MAX(science) FROM students_marks;
SELECT MIN(maths) FROM students_marks WHERE class = "V";
SELECT MAX(science) FROM students_marks WHERE gender = "Female";
```

# Grouping
COUNT, MAX, MIN, SUM, AVG
```js
SELECT COUNT(*) FROM students_marks GROUP BY gender;
SELECT COUNT(*), class, section FROM students_marks GROUP BY class, section;
SELECT AVG(maths), class, section FROM students_marks GROUP BY class, section;
```

# Having

Filters on aggregation
```js
SELECT COUNT(*) as num,gender FROM students_marks GROUP BY gender HAVING num < 400;
SELECT COUNT(*) as num, class, section FROM students_marks GROUP BY class, section HAVING num > 20;
SELECT AVG(maths) as maths_avg, class, section FROM students_marks GROUP BY class, section HAVING maths_avg > 50;
```

# Primary Key & Auto Increment

Primary Key - Unique Identifier
```js
CREATE TABLE users (
    id int NOT NULL AUTO_INCREMENT,
    name varchar(255) NOT NULL,
    PRIMARY KEY (id)
);
```
```js
CREATE TABLE countries (
    id int NOT NULL AUTO_INCREMENT,
    name varchar(255) NOT NULL,
    PRIMARY KEY (id)
);
```

# Foreign Key
```js
CREATE TABLE users (
    id int NOT NULL AUTO_INCREMENT,
    name varchar(255) NOT NULL,
    country_id int,
    PRIMARY KEY (id),
    FOREIGN KEY (country_id) REFERENCES countries(id)
);
```

# Data Types & Functions
Numeric

```js
https://dev.mysql.com/doc/refman/8.0/en/numeric-types.html
https://dev.mysql.com/doc/refman/8.0/en/numeric-functions.html
```

String
```js
https://dev.mysql.com/doc/refman/8.0/en/string-types.html
https://dev.mysql.com/doc/refman/8.0/en/string-functions.html
```

Date & Time
```js
https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html
https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html
```