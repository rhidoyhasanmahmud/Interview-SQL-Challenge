# Interview SQL Challenge

## Challenge - 01 (Problems and Solutions)

#### Tables

![Employee-Department-Table](https://github.com/CodeMechanix/Interview-SQL-Challenge/blob/master/Images/Employee-Department-Table.PNG)

> Problem 01: Return Employee record with max salary.
```sql
SELECT * 
FROM employee
WHERE salary = (SELECT MAX(salary) FROM employee);
```
> Problem 02: Select Highest salary in employee table.
```sql
SELECT MAX(salary) FROM employee;
```
> Problem 03: Select Second Highest Salary in employee table.
```sql
SELECT MAX(salary) 
FROM employee
WHERE salary NOT IN (SELECT MAX(salary) FROM employee)
```
> Problem 04: Select range of Employee based on ID.
```sql
SELECT * 
FROM employee
WHERE employee_id BETWEEN 2000 and 2003;
```
> Problem 05: Return Employee name, highest salary and department.
```sql
SELECT e.first_name, e.last_name, e.salary, d.department_name
FROM employee AS e
INNER JOIN department AS d 
ON (e.department_id = d.department_id)
-- WHERE salary = (SELECT MAX(salary) FROM employee)
WHERE salary IN (SELECT MAX(salary) FROM employee)
```
> Problem 06: Return Highest salary, employee name, department name for each department.
```sql
SELECT e.first_name, e.last_name, e.salary, d.department_name
FROM employee AS e
INNER JOIN department AS d 
ON (e.department_id = d.department_id)
-- WHERE salary = (SELECT MAX(salary) FROM employee  GROUP BY department_id)
WHERE salary IN (SELECT MAX(salary) FROM employee GROUP BY department_id)
```

## Challenge - 02 (Problems and Solutions)

#### Tables

![Student-Table](https://github.com/CodeMechanix/Interview-SQL-Challenge/blob/master/Images/Student-table.PNG)

> Find the ID, Name of all students.
```sql
SELECT ID, Name 
FROM student;
```
> Find the ID, Name of all students of CSE department.
```sql
SELECT ID, Name 
FROM student
WHERE department='CSE';
```
> Find the lowest CGPA from all students.
```sql
SELECT MIN(cgpa) 
FROM student
```
> Find the highest CGPA of CSE department.
```sql
SELECT MAX(cgpa) 
FROM student
WHERE department='CSE';
```
> Find the total number of students of CSE department.
```sql
SELECT COUNT(ID) 
FROM student
WHERE department='CSE';
```

## Challenge - 03 (Problems and Solutions)

#### Tables

![Employee-Table](https://github.com/CodeMechanix/Interview-SQL-Challenge/blob/master/Images/Employee-Table.PNG)

> Fetch the count of employees working in project 'P1'
```sql
SELECT COUNT(*) 
from employee_salary 
WHERE project='P1'
```
> Fetch Employee names having salary greater than or equal to 25000 and less than or equal 35000.
```sql
SELECT name 
FROM employee_details
WHERE id 
IN
(SELECT employee_id 
 FROM employee_salary
 WHERE salary 
 BETWEEN
 25000 AND 35000)
```
```sql
SELECT ed.name 
FROM employee_details AS ed
INNER JOIN employee_salary AS es 
ON ed.id = es.employee_id
WHERE 
(es.salary>=25000 and es.salary<=35000)
```
> Fetch project-wise count of employees sorted by projects count in descending order
```sql
SELECT project, COUNT(employee_id) AS Total_Project
FROM employee_salary
GROUP BY project
ORDER BY Total_Project DESC
```

