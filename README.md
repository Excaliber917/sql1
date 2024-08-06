# SQL


# BASIC

**SQL has mainly three types of**
* DDL(data defination language) - create , alter and drop.
* DML(data manupulation language) - select , insert , update and delete.
* DCL(data control language) - it has two parts :-
     * **Grant Access** where you grant access to someone to work in your db
     * **Revoke Access** where you take back the control.

**Datatypes**
* datatype of a column defines what value the column can store.
* it is defined when the table is created.
* mainly three types:-
  * string:- char , varchar
  * numeric:- int, float
  * boolean:- bool
  * date and time :- date and datetime

**Constraints**
* constraints are use to specify rules on the data in the table.


 
# HOW TO CREATE and DELETE DATABASE ,TABLE, INSERT VALUES IN IT, SET PRIMARY KEY

```
-- Active: 1722719067439@@127.0.0.1@3306@github
CREATE DATABASE IF NOT EXISTS github

USE github



 CREATE TABLE student (
rollno INT PRIMARY KEY,
name VARCHAR(50),
marks INT NOT NULL,
grade VARCHAR(1),
city VARCHAR(20),
dept_id INT
);

INSERT INTO student
(rollno, name, marks, grade, city,dept_id)
VALUES
(101, "anil", 78, "C", "Pune",2),
(102, "bhumika", 93, "A", "Mumbai",2),
(103, "chetan", 85, "B", "Mumbai",1),
(104, "dhruv", 96, "A", "Delhi",3),
(105, "emanuel", 12, "F", "Delhi",4),
(106, "farah", 82, "B", "Delhi",3)

CREATE TABLE dept(
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
)

INSERT INTO dept(dept_id,dept_name) VALUES
(1,"eng"),
(2,"sci"),
(3,"math"),
(4,"beng")

SHOW TABLES

SELECT * FROM student

DROP TABLE IF EXISTS student

SELECT * FROM dept



```
SQL constraints are used to specify rules for data in a table

```
NOT NULL:columns cannot have a null value.
UNIQUE:columns must have a unique values.
PRIMARY KEY:makes a column unique & not null but used only for one
```

# WHERE CLAUSE

```

SELECT * FROM student WHERE marks >40

SELECT * FROM student WHERE marks BETWEEN 70 AND 90

SELECT name,marks, marks+5 as insreased_marks FROM student WHERE marks BETWEEN 60 and 80

SELECT 
    rollno, 
    name, 
    marks
FROM 
    student
WHERE 
    marks > ALL (SELECT marks FROM student WHERE dept_id = 2);


SELECT 
    rollno, 
    name, 
    marks
FROM 
    student
WHERE 
    name LIKE 'a%';

SELECT name,city FROM student WHERE city IN ("mumbai","delhi")
```
# LIMIT CLAUSE

```
SELECT * FROM student LIMIT 3
```

# ORDER BY CLAUSE

```

SELECT name,marks FROM student WHERE marks>70 ORDER BY marks

SELECT name,marks FROM student WHERE marks>70 ORDER BY marks DESC
```

# AGGREGATE FUNCTIONS

```

SELECT AVG(marks) FROM student

SELECT MAX(marks) FROM student

SELECT MIN(marks) FROM student

SELECT COUNT(name) FROM student

SELECT name,marks FROM student WHERE marks > (SELECT AVG(marks) FROM student)
```

# GROUP BY

```

SELECT city FROM student GROUP BY city

SELECT city, COUNT(name) FROM student GROUP BY city

SELECT city,name, MAX(marks) FROM student GROUP BY city,name 

```



# HAVING CLAUSE
```

SELECT city,name, marks FROM student GROUP BY city,name,marks HAVING MAX(marks) > 90

SELECT name,dept_id FROM student GROUP BY name,dept_id HAVING dept_id =2
```


# DIFF BETWEEN HAVING AND WHERE
The HAVING and WHERE clauses in SQL are both used to filter records, but they serve different purposes and are used in different contexts. Here are the main differences between the two:

**WHERE Clause**

* Purpose: The WHERE clause is used to filter rows before any groupings are made. It is applied to individual rows in a table.
Usage: It is used with SELECT, UPDATE, DELETE, etc., to filter rows based on specific conditions.
Aggregate Functions: Aggregate functions cannot be used directly in the WHERE clause.

**HAVING Clause**

* Purpose: The HAVING clause is used to filter groups of rows created by the GROUP BY clause. It is applied after the rows have been grouped.
Usage: It is used with GROUP BY to filter groups based on specific conditions.
Aggregate Functions: Aggregate functions can be used in the HAVING clause to filter groups.

# UPDATE AND SET
```
UPDATE student SET grade = "O" WHERE grade = "A"
```

# DELETE QUERY

```
DELETE FROM student WHERE marks<30

```
# FOREIGN KEY
* A foreign key is a column (or set of columns) in a table that refers to the primary key in another table.
* FKs can have duplicate & null values.
* There can be multiple FKs
* Here we are using cascading so that one table chnage will reflect on other

```


CREATE TABLE department(
    _id INT PRIMARY KEY NOT NULL,
    dept_name VARCHAR(20) UNIQUE NOT NULL
)

DROP TABLE department

INSERT INTO department(_id,dept_name) VALUES
(1,"A"),
(6,"f"),
(5,"s"),
(4,"e"),
(3,"sA"),
(2,"q")



CREATE TABLE emp(
    emp_id INT PRIMARY KEY NOT NULL,
    emp_name VARCHAR(20) NOT NULL,
    salary INT,
    dept_id INT ,
    emp_age INT CHECK(emp_age>=18 AND emp_age<60),
    Foreign Key (dept_id) REFERENCES department(_id)
    ON UPDATE CASCADE
    
);

INSERT INTO emp(emp_id,emp_name,salary,dept_id,emp_age) VALUES
(1,"sd",200,4,25),
(2,"wd",200,1,25),
(3,"gd",200,3,25),
(4,"ed",200,4,25),
(5,"ad",200,4,25),
(6,"sd",200,2,25),
(7,"wd",200,2,25)

UPDATE department SET _id= 10 WHERE _id=1

SELECT * FROM emp

SELECT * FROM department

```
* here in this case the chnage will reflect on the emp table as well

# ALTER

```
ALTER TABLE table_name
ADD COLUMN column_name datatype constraint;

ALTER TABLE table_name
DROP COLUMN column_name;

ALTER TABLE table_name
RENAME TO new_table_name;

ALTER TABLE table_name
CHANGE COLUMN old_name new_name new_datatype new_constraint;

ALTER TABLE table_name
MODIFY col_name new_datatype new_constraint;

```