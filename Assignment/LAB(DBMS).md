

# 1 INTRODUCTION TO SQL



## LAB EXECRISES :





Lab 1: Create a new database named school\_db and a table called students with the following columns: student\_id, student\_name, age, class, and address.



CREATE DATABASE school\_db;



CREATE TABLE students (

&nbsp;   student\_id INT PRIMARY KEY,

&nbsp;   student\_name VARCHAR(100),

&nbsp;   age Big INT,

&nbsp;   class VARCHAR(50),

&nbsp;   address VARCHAR(255)

);





Lab 2: Insert 5 Records and Retrieve All



INSERT INTO students (student\_id, student\_name, age, class, address) VALUES

(1, 'Alice Johnson', 14, '8A', '123 Maple St'),

(2, 'Bob Smith', 15, '9B', '456 Oak Ave'),

(3, 'Charlie Lee', 13, '7C', '789 Pine Rd'),

(4, 'Diana Prince', 14, '8A', '321 Elm St'),

(5, 'Ethan Hunt', 15, '9B', '654 Cedar Blvd');



-- Retrieve all records

SELECT \* FROM students;





# 2 SQL SYNTAX

LAB EXECRISES :





Lab 1: Write SQL queries to retrieve specific columns (student\_name and age) from the students table.



SELECT student\_name, age

FROM students;



Lab 2: Write SQL queries to retrieve all students whose age is greater than 10.



SELECT \* 

FROM students

WHERE age > 10;







# 3 SQL CONSTRAINT



LAB EXCRISES:





Lab 1: Create a table teachers with the following columns: teacher\_id (Primary Key), teacher\_name (NOT NULL), subject (NOT NULL), and email (UNIQUE).



CREATE TABLE teachers (

&nbsp;   teacher\_id INT PRIMARY KEY AUTO\_INCREMENT,

&nbsp;   teacher\_name VARCHAR(100) NOT NULL,

&nbsp;   subject VARCHAR(100) NOT NULL,

&nbsp;   email VARCHAR(100) UNIQUE

);



Lab 2: Implement a FOREIGN KEY constraint to relate the teacher\_id from the teachers table with the students table.



ALTER TABLE students

ADD COLUMN teacher\_id INT;



ALTER TABLE students

ADD CONSTRAINT fk\_teacher

FOREIGN KEY (teacher\_id) REFERENCES teachers(teacher\_id);







# 4 Main SQL Commands and Sub-commands (DDL)



LAB EXCERSIES :





Lab 1: Create a table courses with columns: course\_id, course\_name, and 

course\_credits. Set the course\_id as the primary key.





CREATE TABLE courses (

&nbsp;   course\_id INT PRIMARY KEY,

&nbsp;   course\_name VARCHAR(100),

&nbsp;   course\_credits INT

);





Lab 2: Use the CREATE command to create a database university\_db 



CREATE DATABASE university\_db;





# 5 ALTER Command





LAB EXCERSIES:



Lab 1: Modify the courses table by adding a column course\_duration using the ALTER command.



ALTER TABLE courses

ADD course\_duration INT;



Lab 2: Drop the course\_credits column from the courses table



ALTER TABLE courses

DROP COLUMN course\_credits;





# 6 DROP Command





LAB EXCERSIES:





Lab 1: Drop the teachers table from the school\_db database



DROP TABLE teachers;



Lab 2: Drop the students table from the school\_db database and verify that the table has been removed



-- Drop the table

DROP TABLE students;



-- Verify that it is removed

SHOW TABLES;





# 7 Data Manipulation Language (DML)





LAB EXCERSIES :



Lab 1: Insert three records into the courses table using the INSERT command.





INSERT INTO courses (course\_id, course\_name, course\_duration)

VALUES

(1, 'Computer Science', 4),

(2, 'Mathematics', 3),

(3, 'Physics', 2);





Lab 2: Update the course duration of a specific course using the UPDATE command.





UPDATE courses

SET course\_duration = 5

WHERE course\_id = 1;





Lab 3: Delete a course with a specific course\_id from the courses table using the DELETE command



DELETE FROM courses

WHERE course\_id = 3;





# 8 Data Query Language (DQL)



LAB EXCERSIES:





Lab 1: Retrieve all courses from the courses table using the SELECT statement. 





SELECT \* FROM courses;





Lab 2: Sort the courses based on course\_duration in descending order using ORDER BY





SELECT \* FROM courses

ORDER BY course\_duration DESC;





Lab 3: Limit the results of the SELECT query to show only the top two courses using LIMIT.



SELECT \* FROM courses

ORDER BY course\_duration DESC

LIMIT 2;





# 9 Data Control Language (DCL)



LAB EXCRESIES:





Lab 1: Create two new users user1 and user2 and grant user1 permission to SELECT from the courses table.





-- Create user1 and user2 (with passwords)

CREATE USER 'user1'@'localhost' IDENTIFIED BY 'password1';

CREATE USER 'user2'@'localhost' IDENTIFIED BY 'password2';



-- Grant SELECT privilege on courses table to user1

GRANT SELECT ON university\_db.courses TO 'user1'@'localhost';



-- Apply changes

FLUSH PRIVILEGES;





Lab 2: Revoke the INSERT permission from user1 and give it to user2.



-- Revoke INSERT privilege from user1

REVOKE INSERT ON university\_db.courses FROM 'user1'@'localhost';



-- Grant INSERT privilege to user2

GRANT INSERT ON university\_db.courses TO 'user2'@'localhost';



-- Apply changes

FLUSH PRIVILEGES;





# 10 Transaction Control Language (TCL)





LAB EXCERSIES:





Lab 1: Insert a few rows into the courses table and use COMMIT to save the changes



-- Start transaction

START TRANSACTION;



-- Insert a few rows

INSERT INTO courses (course\_id, course\_name, course\_duration) 

VALUES

(4, 'Chemistry', 3),

(5, 'Biology', 2);



-- Save changes permanently

COMMIT;





Lab 2: Insert additional rows, then use ROLLBACK to undo the last insert operation.





-- Start transaction

START TRANSACTION;



-- Insert additional rows

INSERT INTO courses (course\_id, course\_name, course\_duration) 

VALUES

(6, 'Economics', 4),

(7, 'History', 3);



-- Undo the above inserts

ROLLBACK;





Lab 3: Create a SAVEPOINT before updating the courses table, and use it to roll back specific changes.





-- Start transaction

START TRANSACTION;



-- Create a SAVEPOINT before making updates

SAVEPOINT before\_update;



-- Update course duration

UPDATE courses SET course\_duration = 5 WHERE course\_id = 4;

UPDATE courses SET course\_duration = 6 WHERE course\_id = 5;



-- Roll back only to the SAVEPOINT (undo updates after it)

ROLLBACK TO before\_update;



-- Save remaining changes

COMMIT;







# 11 SQL Joins



LAB EXCERSIES:





lab 1 : Create two tables: departments and employees. Perform an INNER JOIN to display employees along with their respective departments.





-- Create departments table

CREATE TABLE departments (

&nbsp;   dept\_id INT PRIMARY KEY,

&nbsp;   dept\_name VARCHAR(100)

);



-- Create employees table

CREATE TABLE employees (

&nbsp;   emp\_id INT PRIMARY KEY,

&nbsp;   emp\_name VARCHAR(100),

&nbsp;   dept\_id INT,

&nbsp;   FOREIGN KEY (dept\_id) REFERENCES departments(dept\_id)

);



-- Insert sample departments

INSERT INTO departments (dept\_id, dept\_name) VALUES

(1, 'HR'),

(2, 'Finance'),

(3, 'IT');



-- Insert sample employees

INSERT INTO employees (emp\_id, emp\_name, dept\_id) VALUES

(101, 'Alice', 1),

(102, 'Bob', 2),

(103, 'Charlie', 3),

(104, 'David', 1);



-- Perform INNER JOIN (only matching records)

SELECT employees.emp\_id, employees.emp\_name, departments.dept\_name

FROM employees

INNER JOIN departments ON employees.dept\_id = departments.dept\_id;





Lab 2: Use a LEFT JOIN to show all departments, even those without employees



SELECT departments.dept\_id, departments.dept\_name, employees.emp\_name

FROM departments

LEFT JOIN employees ON departments.dept\_id = employees.dept\_id;





# 12 SQL Group By



LAB EXCERSIES:





Lab 1: Group employees by department and count the number of employees in each department using GROUP BY.





SELECT dept\_id, COUNT(emp\_id) AS total\_employees

FROM employees

GROUP BY dept\_id;



Lab 2: Use the AVG aggregate function to find the average salary of employees in each department.



SELECT d.dept\_name, COUNT(e.emp\_id) AS total\_employees

FROM departments d

LEFT JOIN employees e ON d.dept\_id = e.dept\_id

GROUP BY d.dept\_name;







# 13 SQL Stored Procedure



LAB EXCERSISES:



Lab 1: Write a stored procedure to retrieve all employees from the employees table based on department. 





DELIMITER $$



CREATE PROCEDURE GetEmployeesByDepartment(IN deptId INT)

BEGIN

&nbsp;   SELECT emp\_id, emp\_name, dept\_id

&nbsp;   FROM employees

&nbsp;   WHERE dept\_id = deptId;

END $$



DELIMITER ;





CALL GetEmployeesByDepartment(2);





Lab 2: Write a stored procedure that accepts course\_id as input and returns the course details.



DELIMITER $$



CREATE PROCEDURE GetCourseDetails(IN c\_id INT)

BEGIN

&nbsp;   SELECT course\_id, course\_name, course\_duration

&nbsp;   FROM courses

&nbsp;   WHERE course\_id = c\_id;

END $$



DELIMITER ;





CALL GetCourseDetails(1);







# 14 SQL View





LAB EXCERSISES :







Lab 1: Create a view to show all employees along with their department names. 





CREATE VIEW EmployeeDepartmentView AS

SELECT e.emp\_id, e.emp\_name, e.salary, d.dept\_name

FROM employees e

INNER JOIN departments d ON e.dept\_id = d.dept\_id;





SELECT \* FROM EmployeeDepartmentView;







Lab 2: Modify the view to exclude employees whose salaries are below $50,000.





CREATE OR REPLACE VIEW EmployeeDepartmentView AS

SELECT e.emp\_id, e.emp\_name, e.salary, d.dept\_name

FROM employees e

INNER JOIN departments d ON e.dept\_id = d.dept\_id

WHERE e.salary >= 50000;





SELECT \* FROM EmployeeDepartmentView;







# 15 SQL Triggers



LAB EXCERSISES :



Lab 1: Create a trigger to automatically log changes to the employees table when a new employee is added. 





CREATE TABLE employee\_log (

&nbsp;   log\_id INT AUTO\_INCREMENT PRIMARY KEY,

&nbsp;   emp\_id INT,

&nbsp;   emp\_name VARCHAR(100),

&nbsp;   action\_type VARCHAR(50),

&nbsp;   action\_time TIMESTAMP DEFAULT CURRENT\_TIMESTAMP

);





Now Create a Trigger:





DELIMITER $$



CREATE TRIGGER after\_employee\_insert

AFTER INSERT ON employees

FOR EACH ROW

BEGIN

&nbsp;   INSERT INTO employee\_log (emp\_id, emp\_name, action\_type)

&nbsp;   VALUES (NEW.emp\_id, NEW.emp\_name, 'INSERT');

END $$



DELIMITER ;







Lab 2: Create a trigger to update the last\_modified timestamp whenever an employee record is updated.







ALTER TABLE employees

ADD last\_modified TIMESTAMP DEFAULT CURRENT\_TIMESTAMP ON UPDATE CURRENT\_TIMESTAMP;





Now Create a trigger:



DELIMITER $$



CREATE TRIGGER before\_employee\_update

BEFORE UPDATE ON employees

FOR EACH ROW

BEGIN

&nbsp;   SET NEW.last\_modified = CURRENT\_TIMESTAMP;

END $$



DELIMITER ;







# 16 Introduction to PL/SQL



LAB EXCERSIES :





Lab 1: Write a PL/SQL block to print the total number of employees from the employees table





SET SERVEROUTPUT ON;



DECLARE

&nbsp;   total\_employees NUMBER;

BEGIN

&nbsp;   SELECT COUNT(\*) INTO total\_employees

&nbsp;   FROM employees;

&nbsp;   

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Total Employees: ' || total\_employees);

END;

/







Lab 2: Create a PL/SQL block that calculates the total sales from an orders table.





SET SERVEROUTPUT ON;



DECLARE

&nbsp;   total\_sales NUMBER;

BEGIN

&nbsp;   SELECT SUM(total\_amount) INTO total\_sales

&nbsp;   FROM orders;

&nbsp;   

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Total Sales: $' || total\_sales);

END;

/





# 17 PL/SQL Control Structures



LAB EXCERSIES :





Lab 1: Write a PL/SQL block using an IF-THEN condition to check the department of an employee. 







SET SERVEROUTPUT ON;



DECLARE

&nbsp;   v\_emp\_id   employees.emp\_id%TYPE := 101;  -- example employee ID

&nbsp;   v\_dept\_id  employees.dept\_id%TYPE;

BEGIN

&nbsp;   SELECT dept\_id INTO v\_dept\_id

&nbsp;   FROM employees

&nbsp;   WHERE emp\_id = v\_emp\_id;



&nbsp;   IF v\_dept\_id = 1 THEN

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Employee ' || v\_emp\_id || ' works in HR.');

&nbsp;   ELSIF v\_dept\_id = 2 THEN

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Employee ' || v\_emp\_id || ' works in Finance.');

&nbsp;   ELSE

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Employee ' || v\_emp\_id || ' works in another department.');

&nbsp;   END IF;

END;

/







Lab 2: Use a FOR LOOP to iterate through employee records and display their names.







SET SERVEROUTPUT ON;



BEGIN

&nbsp;   FOR emp\_rec IN (SELECT emp\_name FROM employees) LOOP

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Employee Name: ' || emp\_rec.emp\_name);

&nbsp;   END LOOP;

END;

/









# 18 SQL Cursors



LAB EXCERSISES :





Lab 1: Write a PL/SQL block using an explicit cursor to retrieve and display employee details.  





SET SERVEROUTPUT ON;



DECLARE

&nbsp;   -- Declare the cursor

&nbsp;   CURSOR emp\_cursor IS

&nbsp;       SELECT emp\_id, emp\_name, dept\_id, salary

&nbsp;       FROM employees;



&nbsp;   -- Variables to store fetched values

&nbsp;   v\_emp\_id   employees.emp\_id%TYPE;

&nbsp;   v\_emp\_name employees.emp\_name%TYPE;

&nbsp;   v\_dept\_id  employees.dept\_id%TYPE;

&nbsp;   v\_salary   employees.salary%TYPE;

BEGIN

&nbsp;   -- Open the cursor

&nbsp;   OPEN emp\_cursor;



&nbsp;   LOOP

&nbsp;       -- Fetch data into variables

&nbsp;       FETCH emp\_cursor INTO v\_emp\_id, v\_emp\_name, v\_dept\_id, v\_salary;



&nbsp;       -- Exit loop when no more rows

&nbsp;       EXIT WHEN emp\_cursor%NOTFOUND;



&nbsp;       -- Display the data

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('ID: ' || v\_emp\_id || 

&nbsp;                            ', Name: ' || v\_emp\_name ||

&nbsp;                            ', Dept: ' || v\_dept\_id ||

&nbsp;                            ', Salary: ' || v\_salary);

&nbsp;   END LOOP;



&nbsp;   -- Close the cursor

&nbsp;   CLOSE emp\_cursor;

END;

/





Lab 2: Create a cursor to retrieve all courses and display them one by one.







SET SERVEROUTPUT ON;



DECLARE

&nbsp;   -- Declare the cursor

&nbsp;   CURSOR course\_cursor IS

&nbsp;       SELECT course\_id, course\_name, duration

&nbsp;       FROM courses;



&nbsp;   -- Variables to store fetched values

&nbsp;   v\_course\_id   courses.course\_id%TYPE;

&nbsp;   v\_course\_name courses.course\_name%TYPE;

&nbsp;   v\_duration    courses.duration%TYPE;

BEGIN

&nbsp;   -- Open the cursor

&nbsp;   OPEN course\_cursor;



&nbsp;   LOOP

&nbsp;       -- Fetch data into variables

&nbsp;       FETCH course\_cursor INTO v\_course\_id, v\_course\_name, v\_duration;



&nbsp;       -- Exit when no more rows

&nbsp;       EXIT WHEN course\_cursor%NOTFOUND;



&nbsp;       -- Display the data

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Course ID: ' || v\_course\_id || 

&nbsp;                            ', Name: ' || v\_course\_name ||

&nbsp;                            ', Duration: ' || v\_duration);

&nbsp;   END LOOP;



&nbsp;   -- Close the cursor

&nbsp;   CLOSE course\_cursor;

END;

/







# 19 Rollback and Commit Savepoint



LAB EXCERSIES :





Lab 1: Perform a transaction where you create a savepoint, insert records, then rollback to the savepoint.  





-- Start transaction

BEGIN;



-- Insert first record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (101, 'John Doe', 10, 55000);



-- Create a savepoint

SAVEPOINT sp1;



-- Insert another record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (102, 'Jane Smith', 20, 60000);



-- Rollback to the savepoint (Jane's record will be undone)

ROLLBACK TO sp1;



-- Commit remaining changes (only John's record will be saved)

COMMIT;









Lab 2: Commit part of a transaction after using a savepoint and then rollback the remaining changes.







-- Start transaction

BEGIN;



-- Insert first record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (103, 'Alice Brown', 30, 50000);



-- Create savepoint

SAVEPOINT sp2;



-- Insert second record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (104, 'Bob Green', 40, 65000);



-- Commit the first part (Alice will be saved)

COMMIT;



-- Insert another record after commit

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (105, 'Charlie White', 50, 70000);



-- Rollback changes made after the commit (Charlie will be undone)

ROLLBACK;



-- End transaction (optional if already committed/rolled back)

COMMIT;







































