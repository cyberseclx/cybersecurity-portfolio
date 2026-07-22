# Day 30 — TryHackMe: SQL Fundamentals

## Room Information

- **Path:** Cyber Security 101 → Web Hacking
- **Room:** SQL Fundamentals
- **Status:** Completed
- **Estimated room time:** 120 minutes

---

## 1. What Is a Database?

A database is an organised collection of data.

A web application may use a database to store:

- Usernames and password hashes
- Product information
- Orders and payments
- Blog posts
- Logs and security events

### Basic structure

- **Database:** The full collection of related data
- **Table:** Data organised into rows and columns
- **Column:** A specific type of information
- **Row:** One complete record
- **Primary key:** A value that uniquely identifies a row
- **Foreign key:** A field that links one table to another

Example table:

| id | name | category |
|---:|---|---|
| 1 | Nmap | Network Scanner |
| 2 | Wireshark | Packet Analyzer |

---

## 2. Relational and Non-Relational Databases

### Relational databases

Relational databases store information in tables.

Examples:

- MySQL
- MariaDB
- PostgreSQL
- Microsoft SQL Server
- SQLite

They normally use SQL to retrieve and manage data.

### Non-relational databases

Non-relational databases do not always use traditional rows and columns.

They may store:

- Documents
- Key-value pairs
- Graph data
- Wide-column data

Examples include MongoDB and Redis.

---

## 3. What Is SQL?

SQL stands for **Structured Query Language**.

It is used to communicate with relational databases.

SQL can be used to:

- Create databases and tables
- Insert records
- Read records
- Update records
- Delete records
- Filter and sort results
- Group and aggregate data

A basic query:

```sql
SELECT * FROM books;
```

Meaning:

> Return every column and every row from the `books` table.

---

## 4. Database and Table Statements

### Show available databases

```sql
SHOW DATABASES;
```

### Select a database

```sql
USE tools_db;
```

### Show tables

```sql
SHOW TABLES;
```

### View a table's structure

```sql
DESCRIBE hacking_tools;
```

or:

```sql
DESC hacking_tools;
```

### Create a database

```sql
CREATE DATABASE example_db;
```

### Create a table

```sql
CREATE TABLE tools (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    category VARCHAR(100),
    amount INT
);
```

### Remove a table

```sql
DROP TABLE tools;
```

`DROP` permanently removes the table and its data, so it must be used carefully.

---

## 5. CRUD Operations

CRUD means:

- **Create**
- **Read**
- **Update**
- **Delete**

### Create — INSERT

```sql
INSERT INTO tools (name, category, amount)
VALUES ('Nmap', 'Network Scanner', 100);
```

### Read — SELECT

```sql
SELECT * FROM tools;
```

Select particular columns:

```sql
SELECT name, category
FROM tools;
```

### Update — UPDATE

```sql
UPDATE tools
SET amount = 150
WHERE name = 'Nmap';
```

The `WHERE` condition is important. Without it, every row may be updated.

### Delete — DELETE

```sql
DELETE FROM tools
WHERE name = 'Nmap';
```

Without a `WHERE` condition, every row may be deleted.

---

## 6. Filtering with WHERE

The `WHERE` clause limits which rows are returned.

```sql
SELECT *
FROM books
WHERE category = 'Defensive Security';
```

### Comparison operators

```text
=   Equal to
!=  Not equal to
<>  Not equal to
>   Greater than
<   Less than
>=  Greater than or equal to
<=  Less than or equal to
```

Example:

```sql
SELECT name, amount
FROM hacking_tools
WHERE amount > 100;
```

---

## 7. AND, OR, and NOT

### AND

Both conditions must be true.

```sql
SELECT *
FROM books
WHERE category = 'Defensive Security'
AND published_date > '2015-01-01';
```

### OR

At least one condition must be true.

```sql
SELECT *
FROM books
WHERE category = 'Defensive Security'
OR category = 'Offensive Security';
```

### NOT

Reverses a condition.

```sql
SELECT *
FROM books
WHERE NOT category = 'Defensive Security';
```

---

## 8. Exact Matching vs Pattern Matching

### Exact match with `=`

```sql
SELECT *
FROM books
WHERE name = 'Android';
```

This only matches a row whose complete value is exactly `Android`.

It does not match:

```text
Android Security Internals
```

### Pattern matching with `LIKE`

```sql
SELECT *
FROM books
WHERE name LIKE '%Android%';
```

The `%` wildcard means any number of characters.

Patterns:

```sql
LIKE 'Android%'    -- Starts with Android
LIKE '%Android'    -- Ends with Android
LIKE '%Android%'   -- Contains Android anywhere
```

The underscore `_` represents exactly one character:

```sql
LIKE 'Nma_'
```

This could match `Nmap`.

---

## 9. Sorting Results

### Ascending order

```sql
SELECT name, amount
FROM hacking_tools
ORDER BY amount ASC;
```

### Descending order

```sql
SELECT name, amount
FROM hacking_tools
ORDER BY amount DESC;
```

`ASC` is the default.

---

## 10. Limiting Results

```sql
SELECT *
FROM books
LIMIT 5;
```

This returns only five rows.

To find the book with the longest name:

```sql
SELECT name, CHAR_LENGTH(name) AS name_length
FROM books
ORDER BY name_length DESC
LIMIT 1;
```

---

## 11. GROUP BY

`GROUP BY` combines rows that have the same value.

```sql
SELECT category, COUNT(*) AS total
FROM books
GROUP BY category;
```

This counts how many books exist in each category.

---

## 12. HAVING

`HAVING` filters grouped results.

```sql
SELECT category, COUNT(*) AS total
FROM books
GROUP BY category
HAVING COUNT(*) > 2;
```

Difference:

- `WHERE` filters rows before grouping
- `HAVING` filters groups after grouping

---

## 13. Useful Operators

### BETWEEN

```sql
SELECT *
FROM hacking_tools
WHERE amount BETWEEN 100 AND 500;
```

### IN

```sql
SELECT *
FROM books
WHERE category IN ('Defensive Security', 'Offensive Security');
```

### IS NULL

```sql
SELECT *
FROM books
WHERE description IS NULL;
```

### IS NOT NULL

```sql
SELECT *
FROM books
WHERE description IS NOT NULL;
```

### Modulo operator

The modulo operator `%` returns the remainder after division.

```sql
SELECT name, amount
FROM hacking_tools
WHERE amount % 10 != 0;
```

This returns tools whose amount does not end in `0`.

Examples:

```text
169 % 10 = 9
375 % 10 = 5
160 % 10 = 0
```

---

## 14. Aggregate Functions

Aggregate functions calculate a result across multiple rows.

### COUNT

```sql
SELECT COUNT(*)
FROM books;
```

### SUM

```sql
SELECT SUM(amount)
FROM hacking_tools;
```

### AVG

```sql
SELECT AVG(amount)
FROM hacking_tools;
```

### MIN

```sql
SELECT MIN(amount)
FROM hacking_tools;
```

### MAX

```sql
SELECT MAX(amount)
FROM hacking_tools;
```

Maximum name length:

```sql
SELECT MAX(CHAR_LENGTH(name)) AS max_length
FROM books;
```

This returns only the maximum length, not the name itself.

---

## 15. String Functions

### LENGTH

```sql
SELECT LENGTH(name)
FROM books;
```

`LENGTH()` returns the number of bytes.

### CHAR_LENGTH

```sql
SELECT CHAR_LENGTH(name)
FROM books;
```

`CHAR_LENGTH()` returns the number of characters and is safer for multibyte text.

### CONCAT

```sql
SELECT CONCAT(name, ' - ', category)
FROM books;
```

This combines values from the same row.

### GROUP_CONCAT

```sql
SELECT GROUP_CONCAT(name SEPARATOR ' & ')
FROM hacking_tools
WHERE amount % 10 != 0;
```

This combines values from multiple rows into one string.

Difference:

- `CONCAT()` joins values within one row
- `GROUP_CONCAT()` joins values from multiple rows

---

## 16. Other Useful Functions

### UPPER

```sql
SELECT UPPER(name)
FROM books;
```

### LOWER

```sql
SELECT LOWER(name)
FROM books;
```

### ROUND

```sql
SELECT ROUND(AVG(amount), 2)
FROM hacking_tools;
```

### SUBSTRING

```sql
SELECT SUBSTRING(name, 1, 5)
FROM books;
```

---

## 17. Important Mistakes and Corrections

### Mistake 1: Using `%` with `=`

Incorrect:

```sql
SELECT *
FROM books
WHERE name = '%Android%';
```

With `=`, `%` is treated as a normal character.

Correct:

```sql
SELECT *
FROM books
WHERE name LIKE '%Android%';
```

### Mistake 2: Expecting `MAX(LENGTH())` to return the name

This query returns only the largest length:

```sql
SELECT MAX(CHAR_LENGTH(name))
FROM books;
```

To return the actual name:

```sql
SELECT name, CHAR_LENGTH(name) AS name_length
FROM books
ORDER BY name_length DESC
LIMIT 1;
```

### Mistake 3: Confusing `CONCAT` with `GROUP_CONCAT`

Use `CONCAT()` for columns in one row.

Use `GROUP_CONCAT()` for values across several rows.

---

## 18. Cybersecurity Relevance

SQL knowledge is useful in both offensive and defensive security.

### Offensive security

It helps with:

- Understanding SQL injection
- Reading vulnerable application queries
- Identifying unsafe input handling
- Retrieving or modifying exposed data in authorised labs

### Defensive security

It helps with:

- Investigating logs
- Finding suspicious records
- Reviewing account activity
- Applying least-privilege database permissions
- Detecting unsafe application queries
- Understanding how web applications store data

---

## 19. Practical Review

### What did I check?

I practised:

- Selecting databases and tables
- Reading and filtering records
- Exact and partial string matching
- Sorting and limiting results
- Aggregate and string functions
- Modulo-based filtering
- Combining multiple row values

### What did I find?

I found that SQL syntax is highly dependent on selecting the correct operator or function.

Examples:

- `=` performs exact matching
- `LIKE` performs pattern matching
- `MAX()` calculates the highest value
- `GROUP_CONCAT()` joins values from multiple rows

### What does it mean?

Small syntax changes can completely change a query's result. Understanding the goal of each operator is more useful than memorising queries blindly.

### What would I do next?

- Practise SQL queries without looking at notes
- Learn how web applications construct SQL queries
- Continue into SQL injection fundamentals
- Practise identifying unsafe queries in authorised labs

---

## 20. Quick Command Reference

```sql
SHOW DATABASES;
USE database_name;
SHOW TABLES;
DESCRIBE table_name;

SELECT * FROM table_name;
SELECT column1, column2 FROM table_name;

SELECT * FROM table_name WHERE condition;
SELECT * FROM table_name ORDER BY column DESC;
SELECT * FROM table_name LIMIT 1;

SELECT COUNT(*) FROM table_name;
SELECT MAX(column) FROM table_name;
SELECT MIN(column) FROM table_name;
SELECT AVG(column) FROM table_name;
SELECT SUM(column) FROM table_name;

SELECT * FROM table_name WHERE name LIKE '%text%';

SELECT GROUP_CONCAT(name SEPARATOR ' & ')
FROM table_name
WHERE condition;
```

---

## Key Takeaway

SQL is the language used to retrieve and manage data in relational databases. The most important beginner skill is understanding the intent of a query: what data is being selected, how it is filtered, and how the final result is formatted.
