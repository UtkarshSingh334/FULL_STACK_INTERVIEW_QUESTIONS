# 🐬 MySQL - Medium Questions

> **Topics Covered:** SQL Commands (DDL, DML, DQL, DCL, TCL), Joins (INNER, LEFT, RIGHT, FULL, CROSS, SELF), `WHERE` vs `HAVING`, Subqueries vs Common Table Expressions (CTEs), Window Functions (`ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`).

---

### Q1: SQL Joins Master Guide ⭐⭐
**Question:** Explain all types of SQL Joins with syntax and Venn diagram logic.

**Answer:**
1. **INNER JOIN**: Returns records that have matching values in both tables.
2. **LEFT (OUTER) JOIN**: Returns all records from the left table and matched records from the right table (NULL if no match).
3. **RIGHT (OUTER) JOIN**: Returns all records from the right table and matched records from the left table.
4. **FULL (OUTER) JOIN**: Returns all records when there is a match in either left or right table (emulated in MySQL via `UNION` of LEFT and RIGHT joins).
5. **CROSS JOIN**: Cartesian product (every row of Table A paired with every row of Table B).
6. **SELF JOIN**: A regular join in which a table is joined with itself (e.g., Employee and Manager hierarchy).

```sql
-- Employee & Manager Self Join
SELECT e.name AS Employee, m.name AS Manager
FROM Employees e
LEFT JOIN Employees m ON e.manager_id = m.id;
```

---

### Q2: `WHERE` vs `HAVING` Clause
**Question:** What is the difference between `WHERE` and `HAVING` in SQL?

**Answer:**
| Criteria | `WHERE` Clause | `HAVING` Clause |
| :--- | :--- | :--- |
| **Execution Order** | Executes **before** `GROUP BY` | Executes **after** `GROUP BY` and aggregation |
| **Filter Target** | Filters individual table rows | Filters aggregated group results |
| **Aggregate Functions**| Cannot contain aggregate functions (`SUM`, `COUNT`) | Can contain aggregate functions (`COUNT(*) > 5`) |

```sql
SELECT department_id, COUNT(*) AS total_employees, AVG(salary) AS avg_sal
FROM Employees
WHERE status = 'Active'               -- Row filter before grouping
GROUP BY department_id
HAVING AVG(salary) > 60000;          -- Group filter after aggregation
```

---

### Q3: Window Functions: `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`
**Question:** Compare `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`. Write a query to find the 2nd highest salary in each department.

**Answer:**
- `ROW_NUMBER()`: Assigns unique consecutive numbers (1, 2, 3, 4) regardless of duplicate values.
- `RANK()`: Assigns same rank to duplicates, but **skips ranks** (1, 2, 2, 4).
- `DENSE_RANK()`: Assigns same rank to duplicates **without skipping** (1, 2, 2, 3).

```sql
WITH RankedSalaries AS (
  SELECT id, name, department_id, salary,
         DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) as sal_rank
  FROM Employees
)
SELECT * FROM RankedSalaries WHERE sal_rank = 2;
```
