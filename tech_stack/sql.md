# SQL FORMAL SPECIFICATION v8.0.0

## 12 PRIMARY SQL KEYWORDS

### 1. **SELECT** - Query Data
```sql
-- Basic select
SELECT * FROM users;
SELECT name, email FROM users;

-- With where clause
SELECT * FROM users WHERE status = 'active';

-- Distinct values
SELECT DISTINCT country FROM users;

-- Aliases
SELECT u.id, u.name AS user_name FROM users AS u;
```

### 2. **WHERE** - Filtering
```sql
-- Comparison operators
WHERE age > 18
WHERE age >= 18
WHERE price < 100
WHERE name = 'John'
WHERE status != 'inactive'

-- Logical operators
WHERE age > 18 AND status = 'active'
WHERE status = 'active' OR status = 'pending'
WHERE NOT status = 'deleted'

-- BETWEEN
WHERE age BETWEEN 18 AND 65

-- IN
WHERE status IN ('active', 'pending')

-- LIKE
WHERE name LIKE 'John%'
WHERE email LIKE '%@example.com'

-- IS NULL
WHERE deleted_at IS NULL
WHERE deleted_at IS NOT NULL
```

### 3. **JOIN** - Combining Tables
```sql
-- INNER JOIN
SELECT u.name, p.title
FROM users u
INNER JOIN posts p ON u.id = p.user_id

-- LEFT JOIN
SELECT u.name, COUNT(p.id) as post_count
FROM users u
LEFT JOIN posts p ON u.id = p.user_id
GROUP BY u.id

-- RIGHT JOIN
SELECT u.name, c.comment_text
FROM users u
RIGHT JOIN comments c ON u.id = c.user_id

-- FULL OUTER JOIN
SELECT u.name, o.order_id
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id

-- CROSS JOIN
SELECT u.id, p.id FROM users u CROSS JOIN products p
```

### 4. **GROUP BY** - Aggregation
```sql
-- Group and count
SELECT country, COUNT(*) as user_count
FROM users
GROUP BY country

-- Group with multiple columns
SELECT status, country, COUNT(*) as count
FROM users
GROUP BY status, country

-- Having clause (filter groups)
SELECT country, COUNT(*) as count
FROM users
GROUP BY country
HAVING COUNT(*) > 10

-- Aggregate functions
SELECT 
  SUM(amount) as total,
  AVG(amount) as average,
  MIN(amount) as minimum,
  MAX(amount) as maximum,
  COUNT(*) as count
FROM orders
```

### 5. **ORDER BY** - Sorting
```sql
-- Ascending
SELECT * FROM users ORDER BY name ASC

-- Descending
SELECT * FROM users ORDER BY created_at DESC

-- Multiple columns
SELECT * FROM users ORDER BY status ASC, created_at DESC

-- Limit/Offset (pagination)
SELECT * FROM users ORDER BY id LIMIT 10 OFFSET 20
```

### 6. **INSERT** - Add Data
```sql
-- Single row
INSERT INTO users (name, email, status)
VALUES ('John', 'john@example.com', 'active')

-- Multiple rows
INSERT INTO users (name, email) VALUES
('John', 'john@example.com'),
('Jane', 'jane@example.com'),
('Bob', 'bob@example.com')

-- From select
INSERT INTO archive_users
SELECT * FROM users WHERE deleted = true
```

### 7. **UPDATE** - Modify Data
```sql
-- Single column
UPDATE users SET status = 'inactive' WHERE id = 1

-- Multiple columns
UPDATE users SET
  name = 'Jane',
  email = 'jane@example.com',
  updated_at = NOW()
WHERE id = 1

-- Conditional update
UPDATE users SET
  status = CASE
    WHEN age < 18 THEN 'minor'
    WHEN age >= 65 THEN 'senior'
    ELSE 'active'
  END
WHERE status IS NULL
```

### 8. **DELETE** - Remove Data
```sql
-- Delete specific records
DELETE FROM users WHERE id = 1

-- Delete with condition
DELETE FROM users WHERE status = 'deleted' AND deleted_at < DATE_SUB(NOW(), INTERVAL 90 DAY)

-- Delete all (use with caution)
DELETE FROM users
```

### 9. **CREATE** - Create Tables
```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  age INT CHECK (age >= 0 AND age <= 150),
  status ENUM('active', 'inactive') DEFAULT 'active',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- With foreign key
CREATE TABLE posts (
  id INT PRIMARY KEY AUTO_INCREMENT,
  title VARCHAR(255) NOT NULL,
  user_id INT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

### 10. **INDEX** - Performance
```sql
-- Create index
CREATE INDEX idx_email ON users(email);

-- Composite index
CREATE INDEX idx_user_status ON users(user_id, status);

-- Unique index
CREATE UNIQUE INDEX idx_email_unique ON users(email);

-- Drop index
DROP INDEX idx_email ON users;
```

### 11. **TRANSACTION** - ACID Compliance
```sql
START TRANSACTION;
  UPDATE users SET balance = balance - 100 WHERE id = 1;
  UPDATE users SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- With rollback
START TRANSACTION;
  DELETE FROM users WHERE id = 1;
  -- If error:
  ROLLBACK;
  -- If success:
  COMMIT;
```

### 12. **STORED** - Stored Procedures
```sql
-- Create procedure
CREATE PROCEDURE GetUserById(IN userId INT)
BEGIN
  SELECT * FROM users WHERE id = userId;
END;

-- Call procedure
CALL GetUserById(1);

-- Procedure with transaction
CREATE PROCEDURE TransferFunds(
  IN fromId INT,
  IN toId INT,
  IN amount DECIMAL(10, 2)
)
BEGIN
  START TRANSACTION;
  UPDATE users SET balance = balance - amount WHERE id = fromId;
  UPDATE users SET balance = balance + amount WHERE id = toId;
  COMMIT;
END;
```

## BEST PRACTICES
1. Use parameterized queries (prevent SQL injection)
2. Index frequently queried columns
3. Use appropriate data types
4. Normalize database design
5. Use transactions for consistency
6. Monitor query performance
7. Use EXPLAIN for optimization
8. Backup regularly
9. Document schema changes
10. Avoid SELECT *

---
