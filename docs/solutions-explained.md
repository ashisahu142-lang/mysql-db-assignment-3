# Assignment 3 solutions explained

The original numbered questions below are transcribed from the supplied Word document. Each question has one corresponding SQL file in `sql/`.

## Question 1

Write a query to display the name (first_name, last_name) and salary for all employees whose salary is not in the range $10,000 through $15,000.

```sql
SELECT first_name, last_name, salary
FROM employees
WHERE salary NOT BETWEEN 10000 AND 15000;
```

`BETWEEN` includes both endpoints, so `NOT BETWEEN` keeps values below 10,000 or above 15,000.

## Question 2

Write a query to display the name (first_name, last_name) and department ID of all employees in departments 30 or 100 in ascending order.

```sql
SELECT first_name, last_name, department_id
FROM employees
WHERE department_id IN (30, 100)
ORDER BY department_id ASC;
```

`IN` matches either department, and `ORDER BY` sorts the returned rows by department ID.

## Question 3

Write a query to display the name (first_name, last_name) and salary for all employees whose salary is not in the range $10,000 through $15,000 and are in department 30 or 100.

```sql
SELECT first_name, last_name, salary
FROM employees
WHERE salary NOT BETWEEN 10000 AND 15000
  AND department_id IN (30, 100);
```

Both conditions must be true: salary is outside the inclusive range and department is 30 or 100.

## Question 4

Write a query to display the name (first_name, last_name) and hire date for all employees who were hired in 1987.

```sql
SELECT first_name, last_name, hire_date
FROM employees
WHERE hire_date >= '1987-01-01'
  AND hire_date <  '1988-01-01';
```

This inclusive-start, exclusive-end date range includes all hire dates in 1987.

## Question 5

Write a query to display the first_name of all employees who have both "b" and "c" in their first name.

```sql
SELECT first_name
FROM employees
WHERE LOWER(first_name) LIKE '%b%'
  AND LOWER(first_name) LIKE '%c%';
```

The two pattern checks require both letters somewhere in the name; `LOWER` makes matching case-insensitive.

## Question 6

Write a query to display the last name, job, and salary for all employees whose job is that of a Programmer or a Shipping Clerk, and whose salary is not equal to $4,500, $10,000, or $15,000.

```sql
SELECT last_name, job, salary
FROM employees
WHERE job IN ('Programmer', 'Shipping Clerk')
  AND salary NOT IN (4500, 10000, 15000);
```

The role must be one of the two listed, and salary must differ from each excluded amount.

## Question 7

Write a query to display the last name of employees whose names have exactly 6 characters.

```sql
SELECT last_name
FROM employees
WHERE CHAR_LENGTH(last_name) = 6;
```

`CHAR_LENGTH` counts characters and keeps only six-character last names.

## Question 8

Write a query to display the last name of employees having 'e' as the third character.

```sql
SELECT last_name
FROM employees
WHERE LOWER(last_name) LIKE '__e%';
```

The two underscores match the first two characters; `e` must be third, with any remaining characters after it.

## Question 9

Write a query to display the jobs/designations available in the employees table.

```sql
SELECT DISTINCT job
FROM employees
WHERE job IS NOT NULL
ORDER BY job ASC;
```

`DISTINCT` removes duplicate job names; NULL entries are excluded and the list is sorted.

## Question 10

Write a query to display the name (first_name, last_name), salary and PF (15% of salary) of all employees.

```sql
SELECT first_name, last_name, salary, salary * 0.15 AS PF
FROM employees;
```

The calculated column `PF` is 15 percent of each employee salary.

## Question 11

Write a query to select all record from employees where last name in 'BLAKE', 'SCOTT', 'KING' and 'FORD'.

```sql
SELECT *
FROM employees
WHERE UPPER(last_name) IN ('BLAKE', 'SCOTT', 'KING', 'FORD');
```

`IN` returns rows matching any listed surname; `UPPER` makes the comparison case-insensitive.
