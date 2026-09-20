# 🐬 MySQL - Medium Interview Questions & Solutions

---

### Q1: Visual Breakdown of SQL JOINs
**Answer:**
- **`INNER JOIN`**: Returns records with matching values in both tables.
- **`LEFT JOIN` (or LEFT OUTER)**: Returns all records from left table, and matched records from right table (fills `NULL` if no match).
- **`RIGHT JOIN`**: Returns all records from right table, and matched records from left table.
- **`FULL OUTER JOIN`**: Returns all records when there is a match in either left or right table (In MySQL, simulated using `LEFT JOIN UNION RIGHT JOIN`).

```sql
-- Fetch all employees with their department names (including employees without department)
SELECT 
  e.employee_id, 
  e.first_name, 
  d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;
```

---

### Q2: Common Table Expressions (CTEs) vs Subqueries
**Answer:**
A CTE (`WITH` clause) defines a temporary named result set within a single query, providing superior readability and recursion capability compared to deeply nested subqueries.

```sql
-- CTE Example: Find employees earning more than their department's average
WITH DeptAvg AS (
  SELECT department_id, AVG(salary) AS avg_salary
  FROM employees
  GROUP BY department_id
)
SELECT e.first_name, e.salary, da.avg_salary
FROM employees e
JOIN DeptAvg da ON e.department_id = da.department_id
WHERE e.salary > da.avg_salary;
```

---

### Q3: Analyzing Queries with `EXPLAIN`
**Answer:**
`EXPLAIN SELECT ...` reveals how MySQL executes a query:
- **`type`**: `ALL` (Full table scan - bad), `index` (Full index scan), `range` (Index range scan - good), `ref` (Non-unique index lookup - good), `const`/`eq_ref` (Primary key lookup - fastest).
- **`possible_keys`**: Indexes MySQL could use.
- **`key`**: Index MySQL actually chose.
- **`rows`**: Estimated number of rows MySQL must examine.
