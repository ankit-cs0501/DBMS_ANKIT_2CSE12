#  DBMS LAB Expeirment 04

> **Date:** 11/February/2026  
> **Database:** Ankit kumar  
> **Server:** MariaDB 10.4.32

---

## Objective

Perform advanced SQL queries on the **EMPLOYEE** table using date functions, pattern matching, string functions, computed columns, and DML operations:

### Q1. Display the list of employees who have joined the company before 30th june 80 or after 31st dec 81.
```sql
SELECT *
FROM EMPLOYEE
WHERE HIREDATE < '1980-06-30'
   OR HIREDATE > '1981-12-31';
```
**Output:**
```
+-------+--------+---------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+---------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK   | 7902 | 1980-12-17 |  800 | NULL |     20 |
|  7788 | SCOTT  | ANALYST | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7876 | ADAMS  | CLERK   | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7934 | MILLER | CLERK   | 7782 | 1982-01-23 | 1300 | NULL |     10 |
+-------+--------+---------+------+------------+------+------+--------+
4 rows in set (0.001 sec)
```
### Q2. Display the name of employees whose name have second alphabet A in their names.
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```
**Output:**
```
+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.001 sec)
```
### Q3. Display the names of employees whose name have second alphabet A in their names.
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE LENGTH(ENAME) = 5;
```
**Output:**
```
+-------+
| ENAME |
+-------+
| SMITH |
| ALLEN |
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| ADAMS |
| JAMES |
+-------+
8 rows in set (0.001 sec)
```
### Q4. Display the names of employees whose names have second alphabet  A in their name.
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '%A_';
```
**Output:**
```
+--------+
| ENAME  |
+--------+
| BLAKE  |
| ADAMS  |
+--------+
2 rows in set (0.001 sec)
```
### Q5. display the names of employees who are not working as salesman or clerk or analyst.
```sql
SELECT ENAME, JOB
FROM EMPLOYEE
WHERE JOB NOT IN ('SALESMAN', 'CLERK', 'ANALYST');
```
**Output:**
```
+-------+-----------+
| ENAME | JOB       |
+-------+-----------+
| JONES | MANAGER   |
| BLAKE | MANAGER   |
| CLARK | MANAGER   |
| KING  | PRESIDENT |
+-------+-----------+
4 rows in set (0.001 sec)
```
### Q6. Display the name of the employee along with their annual salary (sal*12). The name of the employee earning highest salary should appear first.
```sql
SELECT ENAME, SAL * 12 AS ANNUAL_SALARY
FROM EMPLOYEE
ORDER BY ANNUAL_SALARY DESC;
```
**Output:**
```
+--------+---------------+
| ENAME  | ANNUAL_SALARY |
+--------+---------------+
| KING   |         60000 |
| SCOTT  |         36000 |
| FORD   |         36000 |
| JONES  |         35700 |
| BLAKE  |         34200 |
| CLARK  |         29400 |
| ALLEN  |         19200 |
| TURNER |         18000 |
| MILLER |         15600 |
| WARD   |         15000 |
| MARTIN |         15000 |
| ADAMS  |         13200 |
| JAMES  |         11400 |
| SMITH  |          9600 |
+--------+---------------+
14 rows in set (0.001 sec)
```
### Q7. Display name, sal, hra, pf, da, totalsal for each employee. The output should be in the order of total sal, hra 15% of sal, da 10% of sal, pf 5% of sal. Total salary will be (sal*hra*da)-pf.
```sql
SELECT ENAME,
       SAL,
       SAL * 0.15 AS HRA,
       SAL * 0.05 AS PF,
       SAL * 0.10 AS DA,
       (SAL + SAL * 0.15 + SAL * 0.10) - SAL * 0.05 AS TOTALSAL
FROM EMPLOYEE;
```
**Output:**
```
+--------+------+---------+---------+---------+----------+
| ENAME  | SAL  | HRA     | PF      | DA      | TOTALSAL |
+--------+------+---------+---------+---------+----------+
| SMITH  |  800 | 120.00  |  40.00  |  80.00  |   960.00 |
| ALLEN  | 1600 | 240.00  |  80.00  | 160.00  |  1920.00 |
| WARD   | 1250 | 187.50  |  62.50  | 125.00  |  1500.00 |
| JONES  | 2975 | 446.25  | 148.75  | 297.50  |  3570.00 |
| MARTIN | 1250 | 187.50  |  62.50  | 125.00  |  1500.00 |
| BLAKE  | 2850 | 427.50  | 142.50  | 285.00  |  3420.00 |
| CLARK  | 2450 | 367.50  | 122.50  | 245.00  |  2940.00 |
| SCOTT  | 3000 | 450.00  | 150.00  | 300.00  |  3600.00 |
| KING   | 5000 | 750.00  | 250.00  | 500.00  |  6000.00 |
| TURNER | 1500 | 225.00  |  75.00  | 150.00  |  1800.00 |
| ADAMS  | 1100 | 165.00  |  55.00  | 110.00  |  1320.00 |
| JAMES  |  950 | 142.50  |  47.50  |  95.00  |  1140.00 |
| FORD   | 3000 | 450.00  | 150.00  | 300.00  |  3600.00 |
| MILLER | 1300 | 195.00  |  65.00  | 130.00  |  1560.00 |
+--------+------+---------+---------+---------+----------+
14 rows in set (0.001 sec)
```
### Q8. Update the salary of each employee by 10% increment who are not eligible for commission.
```sql
UPDATE EMPLOYEE
SET SAL = SAL * 1.10
WHERE COMM IS NULL;
```
**Output:**
```
Query OK, 9 rows affected (0.003 sec)
Rows matched: 9  Changed: 9  Warnings: 0
```
### Q9. Display those employees whose salary is more than 3000 after giving 20% increment.
```sql
SELECT ENAME, SAL, SAL * 1.20 AS SAL_AFTER_INCREMENT
FROM EMPLOYEE
WHERE SAL * 1.20 > 3000;
```
**Output:**
```
+-------+------+---------------------+
| ENAME | SAL  | SAL_AFTER_INCREMENT |
+-------+------+---------------------+
| JONES | 2975 |             3570.00 |
| BLAKE | 2850 |             3420.00 |
| SCOTT | 3000 |             3600.00 |
| KING  | 5000 |             6000.00 |
| FORD  | 3000 |             3600.00 |
+-------+------+---------------------+
5 rows in set (0.001 sec)
```
### Q10. Display those employees whose salary contains atleast 3 digits
```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL >= 100;
```
**Output:**
```
+--------+------+
| ENAME  | SAL  |
+--------+------+
| SMITH  |  800 |
| ALLEN  | 1600 |
| WARD   | 1250 |
| JONES  | 2975 |
| MARTIN | 1250 |
| BLAKE  | 2850 |
| CLARK  | 2450 |
| SCOTT  | 3000 |
| KING   | 5000 |
| TURNER | 1500 |
| ADAMS  | 1100 |
| JAMES  |  950 |
| FORD   | 3000 |
| MILLER | 1300 |
+--------+------+
14 rows in set (0.001 sec)
```
## Name : Ankit kumar (2410031066) ### 