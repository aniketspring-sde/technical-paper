## SQL JOINS
- JOIN statements allow us to access information from two or more tables at once. They also keep our database normalized.

### Types of Joins :
- INNER JOIN - It returns dataset that have matching values in both tables.
- LEFT JOIN - It returns all records from the left table and matched records from the right.
- RIGHT JOIN - It returns all records from the right table and matched records from the left.
- FULL JOIN - It returns all records when there is a match in either the left table or the right table.

## Aggregations
- Aggregations mean summarizing the set of values into single value.
  #### Common aggregate functions are:
   COUNT(), SUM(), AVG(), MIN(), MAX()

## Filters

Filtering means selecting only the rows that satisfy a specified condition.

### Filtering Clauses

- `WHERE` – Filters rows before grouping.
- `HAVING` – Filters groups after `GROUP BY`.
- `IN` – Matches a value against a list of values.
- `BETWEEN` – Filters values within a specified range.
- `LIKE` – Searches for a specified pattern.
- `IS NULL` – Checks whether a value is `NULL`.
- `IS NOT NULL` – Checks whether a value is not `NULL`.

### Filtering Operators

| Operator | Description |
|---|---|
| `=` | Equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |
| `<>` | Not equal to |
```
  SELECT * FROM employees
  WHERE department_id IN (10, 20);
```
```
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 70000;
```
