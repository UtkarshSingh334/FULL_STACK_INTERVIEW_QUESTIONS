# 🐬 SQL - Top 17 Essential Interview Queries

> **Practical Interview Queries:** Second-highest salary, Nth-highest salary, Duplicates, Department max salary, Joins, Top 3 salaries per department, `GROUP BY` vs `HAVING`, Window Functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`), CTEs vs Subqueries.

---

### 1. Find the Second-Highest Salary
```sql
-- Approach 1: Subquery with MAX
SELECT MAX(salary) AS SecondHighestSalary
FROM Employees
WHERE salary < (SELECT MAX(salary) FROM Employees);

-- Approach 2: DENSE_RANK Window Function (Recommended)
WITH RankedSalaries AS (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
  FROM Employees
)
SELECT salary FROM RankedSalaries WHERE rnk = 2 LIMIT 1;
```

---

### 2. Find the Nth-Highest Salary (e.g. N = 4)
```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N = N - 1;
  RETURN (
    SELECT DISTINCT salary FROM Employees
    ORDER BY salary DESC
    LIMIT 1 OFFSET N
  );
END;
```

---

### 3. Find Duplicate Records in a Table
```sql
SELECT email, COUNT(*) AS count
FROM Users
GROUP BY email
HAVING COUNT(*) > 1;
```

---

### 4. Delete Duplicate Records (Keeping the lowest ID)
```sql
DELETE u1 FROM Users u1
INNER JOIN Users u2
ON u1.email = u2.email AND u1.id > u2.id;
```

---

### 5. Find Employees Earning More Than Their Department Average
```sql
SELECT e.id, e.name, e.salary, e.department_id
FROM Employees e
WHERE e.salary > (
  SELECT AVG(salary)
  FROM Employees
  WHERE department_id = e.department_id
);
```

---

### 6. Find Department-Wise Maximum Salary
```sql
SELECT department_id, MAX(salary) AS max_salary
FROM Employees
GROUP BY department_id;
```

---

### 7. Find Employees Without a Department (Unassigned)
```sql
SELECT e.id, e.name
FROM Employees e
LEFT JOIN Departments d ON e.department_id = d.id
WHERE d.id IS NULL;
```

---

### 8. Find Customers Who Never Placed an Order
```sql
SELECT c.id, c.name
FROM Customers c
LEFT JOIN Orders o ON c.id = o.customer_id
WHERE o.id IS NULL;
```

---

### 9. Find the Top 3 Highest Salaries in Every Department
```sql
WITH RankedDepartmentSalaries AS (
  SELECT id, name, department_id, salary,
         DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rnk
  FROM Employees
)
SELECT id, name, department_id, salary, rnk
FROM RankedDepartmentSalaries
WHERE rnk <= 3;
```

---

### 10. `GROUP BY` vs `HAVING` Example
```sql
SELECT department_id, COUNT(*) AS total_staff, AVG(salary) AS avg_sal
FROM Employees
WHERE status = 'ACTIVE'               -- Filters rows before grouping
GROUP BY department_id
HAVING COUNT(*) >= 5 AND AVG(salary) > 50000; -- Filters groups after aggregation
```

---

### 11. Window Functions: `ROW_NUMBER()` vs `RANK()` vs `DENSE_RANK()`
| Function | Duplicate Handling | Sequence Output for Salaries [100, 100, 80, 70] |
| :--- | :--- | :--- |
| **`ROW_NUMBER()`** | Assigns unique consecutive numbers | 1, 2, 3, 4 |
| **`RANK()`** | Assigns same rank, skips next rank | 1, 1, 3, 4 (skips 2) |
| **`DENSE_RANK()`** | Assigns same rank, does **not** skip | 1, 1, 2, 3 |

```sql
SELECT name, salary,
       ROW_NUMBER() OVER(ORDER BY salary DESC) as row_num,
       RANK() OVER(ORDER BY salary DESC) as rnk,
       DENSE_RANK() OVER(ORDER BY salary DESC) as dense_rnk
FROM Employees;
```

---

### 12. Common Table Expressions (CTE) vs Subqueries
- **Subquery**: Nested query embedded inside a `SELECT`, `FROM`, or `WHERE` clause. Can be hard to read when deeply nested.
- **CTE (`WITH clause`)**: Temporary named result set defined before the main query. Improves readability, can be referenced multiple times, and supports **Recursive CTEs** (e.g. hierarchical employee manager trees).

```sql
-- Recursive CTE to print numbers 1 to 5:
WITH RECURSIVE NumberSequence AS (
  SELECT 1 AS n
  UNION ALL
  SELECT n + 1 FROM NumberSequence WHERE n < 5
)
SELECT * FROM NumberSequence;
```
