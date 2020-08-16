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
