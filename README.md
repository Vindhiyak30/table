CREATE DATABASE company_db;
USE company_db;

CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
INSERT INTO departments VALUES
(1,'HR'),
(2,'IT'),
(3,'Finance');

INSERT INTO employees VALUES
(101,'Arun',30000,1),
(102,'Bala',40000,2),
(103,'Charan',35000,2),
(104,'Divya',50000,3),
(105,'Ezhil',28000,NULL);

SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;


SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;

SELECT e.emp_name, d.dept_name
FROM employees e
RIGHT JOIN departments d
ON e.dept_id = d.dept_id;

SELECT e.emp_name, d.dept_name
FROM employees e
CROSS JOIN departments d;

SELECT emp_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

SELECT emp_name
FROM employees
WHERE dept_id = (
    SELECT dept_id
    FROM departments
    WHERE dept_name = 'IT'
);

SELECT e.emp_name, d.dept_name
FROM employees e
JOIN departments d
ON e.dept_id = d.dept_id
WHERE e.salary = (
    SELECT MAX(salary)
    FROM employees
);

SELECT d.dept_name,
       (SELECT AVG(e.salary)
        FROM employees e
        WHERE e.dept_id = d.dept_id) AS avg_salary
FROM departments d;
