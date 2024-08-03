# SQL


# BASIC

LIKE HOW TO CREATE DATABASE ,TABLE, INSERT ,DELETE , PRIMARY KEY AND FOREIGN

CREATE DATABASE IF NOT EXISTS student;

USE student;

CREATE TABLE student (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);

INSERT INTO student VALUES (1, 'dj', 'kol');


CREATE TABLE city (
    id INT PRIMARY KEY,
    city_name VARCHAR(50),
    FOREIGN KEY (id) REFERENCES student(id)
);

INSERT INTO city VALUES (1, 'kol');


SELECT * FROM student;
SELECT * FROM city;


DROP TABLE student;
