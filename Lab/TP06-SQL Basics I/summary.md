# TP06 — SQL Basics I

# Exercise 1 — Strong and Weak Entities

| Entity       | Type   | Reason                                    |
| ------------ | ------ | ----------------------------------------- |
| customers    | Strong | Has its own primary key                   |
| employees    | Strong | Exists independently                      |
| offices      | Strong | Independent table                         |
| productlines | Strong | Has its own identifier                    |
| products     | Strong | Exists without depending on another table |
| orders       | Strong | Has its own primary key                   |
| orderdetails | Weak   | Depends on orders and products            |
| payments     | Weak   | Depends on customers                      |

---

# Exercise 2 — Relationships

| Relationship                      | Type                   |
| --------------------------------- | ---------------------- |
| customers → orders                | One-to-Many            |
| customers → payments              | One-to-Many            |
| employees → customers             | One-to-Many            |
| offices → employees               | One-to-Many            |
| productlines → products           | One-to-Many            |
| orders → orderdetails             | One-to-Many            |
| products → orderdetails           | One-to-Many            |
| employees → employees (reportsTo) | Recursive Relationship |

---

# Exercise 3 — Relationship Cardinalities

| Table A      | Table B      | Cardinality |
| ------------ | ------------ | ----------- |
| customers    | orders       | 1:N         |
| customers    | payments     | 1:N         |
| employees    | customers    | 1:N         |
| offices      | employees    | 1:N         |
| productlines | products     | 1:N         |
| orders       | orderdetails | 1:N         |
| products     | orderdetails | 1:N         |
| employees    | employees    | 1:N         |

---

# Exercise 4 — Questions

## 1. Why is `orderdetails` considered a weak entity?

Because it cannot exist without both an order and a product. It depends on those tables to make sense.

## 2. What is the purpose of the `reportsTo` field in employees?

It shows which employee is the manager or supervisor of another employee.

## 3. Why do databases use primary keys?

Primary keys make each row unique and help connect tables together.

---

# Exercise 5 — Display Entire Tables

```sql
USE classicmodels;

SELECT * FROM customers;
SELECT * FROM products;
SELECT * FROM employees;
```

---

# Exercise 6 — Display Specific Columns

```sql
SELECT customerName, city FROM customers;

SELECT productName, buyPrice FROM products;

SELECT firstName, lastName, jobTitle FROM employees;
```

---

# Exercise 7 — Using WHERE Conditions

```sql
SELECT * FROM customers
WHERE country = 'France';

SELECT * FROM customers
WHERE country = 'USA';

SELECT * FROM products
WHERE buyPrice < 50;

SELECT * FROM products
WHERE quantityInStock > 5000;

SELECT * FROM employees
WHERE jobTitle = 'Sales Rep';
```

---

# Exercise 8 — Multiple Conditions

```sql
SELECT * FROM customers
WHERE country = 'USA'
AND creditLimit > 100000;

SELECT * FROM products
WHERE productLine = 'Classic Cars'
AND buyPrice > 80;
```

---

# Exercise 9 — INSERT

```sql
INSERT INTO customers (
    customerNumber,
    customerName,
    contactLastName,
    contactFirstName,
    phone,
    addressLine1,
    city,
    country,
    creditLimit
)
VALUES (
    999,
    'My Test Company',
    'Smith',
    'John',
    '0123456789',
    '123 Test Street',
    'Phnom Penh',
    'Cambodia',
    50000
);

SELECT * FROM customers
WHERE customerNumber = 999;
```

---

# Exercise 10 — UPDATE

```sql
UPDATE customers
SET city = 'Siem Reap'
WHERE customerNumber = 999;

UPDATE customers
SET creditLimit = 75000
WHERE customerNumber = 999;

SELECT * FROM customers
WHERE customerNumber = 999;
```

---

# Exercise 11 — DELETE

```sql
DELETE FROM customers
WHERE customerNumber = 999;

SELECT * FROM customers
WHERE customerNumber = 999;
```

---