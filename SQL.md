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
## Normalization
- Normalization is a process of reducing redundancy by organizing the data into multiple tables. Normalization leads to better usage of disk spaces and makes it easier to maintain the integrity of the      database.
#### Types of normalization forms in a DBMS:

  - 1NF: It is known as the first normal form and is the simplest type of normalization that you can implement in a database. A table to be in its first normal form should satisfy the following conditions:

    - Every column must have a single value and should be atomic.
    - Duplicate columns from the same table should be removed.
    - Separate tables should be created for each group of related data and each row should be identified with a unique column.
  - 2NF: It is known as the second normal form. A table to be in its second normal form should satisfy the following conditions:

    - The table should be in its 1NF, satisfy all the conditions of 1NF.     
    - Every non-prime attribute of the table should be fully functionally dependent on the primary key i.e. every non-key attribute should be dependent on the primary key in such a way that if any key element is deleted, then even the non-key element will be saved in the database.
  - 3NF: It is known as the third normal form. A table to be in its third normal form should satisfy the following conditions:

    - The table should be in its 2NF i.e. satisfy all the conditions of 2NF.
    - There is no transitive functional dependency of one attribute on any attribute in the same table.
  - BCNF: BCNF stands for Boyce-Codd Normal Form and is an advanced form of 3NF. It is also referred to as 3.5NF for the same reason. A table to be in its BCNF normal form should satisfy the following conditions:

    - The table should be in its 3NF i.e. satisfy all the conditions of 3NF.
    - For every functional dependency of any attribute A on B
    (A->B), A should be the super key of the table. It simply implies that A can’t be a non-prime attribute if B is a prime attribute.






## Lock 

- A database lock is a mechanism to protect a shared piece of data from getting updated by two or more database users at the same time. When a single database user or session has acquired a lock then no other database user or session can modify that data until the lock is released.

    - Shared Lock: A shared lock is required for reading a data item and many transactions may hold a lock on the same data item in a shared lock. Multiple transactions are allowed to read the data items in a shared lock.
  - Exclusive lock: An exclusive lock is a lock on any transaction that is about to perform a write operation. This type of lock doesn’t allow more than one transaction and hence prevents any inconsistency in the database. 


## Indexes
- An index in DBMS is used to speed up data retrieval.

  #### Types of indexes :

    - Primary Index -It is created on a sorted data file, usually on the primary key.
    - Clustered Index - This one determines the physical order of data in the table, only one allowed.
    - Secondary Index - Created on non-primary key columns for faster access.
    - Non-clustered Index - Separate structure storing pointers to actual data.

    - B-Tree Index - Balanced tree structure, most commonly used.
    - B+ Tree Index - An improved version of the B-Tree, stores data only in leaf nodes.
    - Hash Index - Uses hash functions, very fast for equality searches.
## Transactions
- A transaction is a sequence of one or more database operations that are treated as one logical unit of work. Either all operations in a transaction succeed, or none of them should take effect.
  #### Transaction Commands

    - BEGIN	- Starts a transaction
    - START - TRANSACTION	Starts a transaction
    - COMMIT - Permanently saves changes
    - ROLLBACK -	Undoes uncommitted changes
    - SAVEPOINT	- Creates a point that can be rolled back to
    - ROLLBACK TO SAVEPOINT -	Rolls back to a specific savepoint

  #### Transaction Example

```sql
    BEGIN;
      UPDATE accounts
      SET balance = balance - 1000
      WHERE id = 1;
      
      UPDATE accounts
      SET balance = balance + 1000
      WHERE id = 2;
      
      COMMIT;
```
 

- If both operations succeed, COMMIT permanently saves the changes.


```sql
    BEGIN;
    
    UPDATE accounts
    SET balance = balance - 1000
    WHERE id = 1;
    
    UPDATE accounts
    SET balance = balance + 1000
    WHERE id = 2;
    
    ROLLBACK;
```

- ROLLBACK cancels the changes made during the transaction.
