Certainly! Here's a comprehensive set of SQL queries covering each concept related to the `Employees` table. I'll explain each concept with a query for you to make clear revision notes.

### 1. **Creating the Table**
```sql
CREATE TABLE Employees (
    employeeID INT PRIMARY KEY,
    firstName VARCHAR(50),
    lastName VARCHAR(50),
    hireDate DATE,
    hourlyPaid DECIMAL(5, 2),
    contactDetails VARCHAR(100),
    mailID VARCHAR(100)
);
```

### 2. **Basic SQL Queries**
#### a. **SELECT Statement**
To select all records from the table:
```sql
SELECT * FROM Employees;
```

#### b. **INSERT INTO**
To insert a new employee:
```sql
INSERT INTO Employees (employeeID, firstName, lastName, hireDate, hourlyPaid, contactDetails, mailID)
VALUES (101, 'John', 'Doe', '2021-01-15', 25.50, '123-456-7890', 'john.doe@example.com');
```

#### c. **UPDATE Statement**
To update an employee's hourly paid:
```sql
UPDATE Employees
SET hourlyPaid = 30.00
WHERE employeeID = 101;
```

#### d. **DELETE Statement**
To delete an employee from the table:
```sql
DELETE FROM Employees
WHERE employeeID = 101;
```

---

### 3. **Filtering and Conditional Queries**
#### a. **WHERE Clause**
To select employees hired after 2020:
```sql
SELECT * FROM Employees
WHERE hireDate > '2020-01-01';
```

#### b. **LIKE Operator**
To select employees whose first name starts with 'J':
```sql
SELECT * FROM Employees
WHERE firstName LIKE 'J%';
```

#### c. **BETWEEN Operator**
To find employees hired between two dates:
```sql
SELECT * FROM Employees
WHERE hireDate BETWEEN '2020-01-01' AND '2023-01-01';
```

#### d. **IN Operator**
To find employees with specific IDs:
```sql
SELECT * FROM Employees
WHERE employeeID IN (101, 102, 103);
```

---

### 4. **Sorting and Limiting Results**
#### a. **ORDER BY Clause**
To get employees sorted by hire date:
```sql
SELECT * FROM Employees
ORDER BY hireDate DESC;
```

#### b. **LIMIT Clause**
To get only the first 5 employees:
```sql
SELECT * FROM Employees
ORDER BY employeeID
LIMIT 5;
```

---

### 5. **Aggregating Data**
#### a. **COUNT Function**
To count the number of employees:
```sql
SELECT COUNT(*) AS totalEmployees FROM Employees;
```

#### b. **SUM Function**
To get the total hourly paid to employees:
```sql
SELECT SUM(hourlyPaid) AS totalHourlyPaid FROM Employees;
```

#### c. **AVG Function**
To calculate the average hourly rate:
```sql
SELECT AVG(hourlyPaid) AS avgHourlyPaid FROM Employees;
```

#### d. **MIN and MAX Functions**
To find the minimum and maximum hourly rates:
```sql
SELECT MIN(hourlyPaid) AS minHourlyPaid, MAX(hourlyPaid) AS maxHourlyPaid FROM Employees;
```

---

### 6. **Joins and Relationships (Hypothetical Tables)**
If you have another table `Departments`:
```sql
CREATE TABLE Departments (
    departmentID INT PRIMARY KEY,
    departmentName VARCHAR(50)
);
```

To join `Employees` and `Departments` on `employeeID` and `departmentID` (assuming a foreign key exists):
```sql
SELECT E.employeeID, E.firstName, D.departmentName
FROM Employees E
INNER JOIN Departments D ON E.departmentID = D.departmentID;
```

---

### 7. **Subqueries**
#### a. **Simple Subquery**
To find employees who earn more than the average hourly rate:
```sql
SELECT * FROM Employees
WHERE hourlyPaid > (SELECT AVG(hourlyPaid) FROM Employees);
```

#### b. **Correlated Subquery**
To find employees hired later than at least one other employee:
```sql
SELECT * FROM Employees E1
WHERE hireDate > (SELECT MIN(hireDate) FROM Employees E2 WHERE E2.employeeID != E1.employeeID);
```

---

### 8. **Group By and Having**
#### a. **GROUP BY Clause**
To group employees by their hourly pay:
```sql
SELECT hourlyPaid, COUNT(*) AS numEmployees
FROM Employees
GROUP BY hourlyPaid;
```

#### b. **HAVING Clause**
To find hourly rates with more than 3 employees:
```sql
SELECT hourlyPaid, COUNT(*) AS numEmployees
FROM Employees
GROUP BY hourlyPaid
HAVING COUNT(*) > 3;
```

---

### 9. **Indexing**
To create an index on `lastName` for faster search:
```sql
CREATE INDEX idx_lastName ON Employees(lastName);
```

---

### 10. **Transactions**
#### a. **Starting a Transaction**
To begin a transaction, insert a new record, and then commit it:
```sql
START TRANSACTION;

INSERT INTO Employees (employeeID, firstName, lastName, hireDate, hourlyPaid, contactDetails, mailID)
VALUES (102, 'Jane', 'Smith', '2022-03-10', 28.00, '555-1234', 'jane.smith@example.com');

COMMIT;
```

#### b. **ROLLBACK**
To revert changes in a transaction:
```sql
START TRANSACTION;

INSERT INTO Employees (employeeID, firstName, lastName, hireDate, hourlyPaid, contactDetails, mailID)
VALUES (103, 'Robert', 'Johnson', '2023-04-12', 30.00, '987-6543', 'robert.johnson@example.com');

ROLLBACK;
```

---

### 11. **Views**
To create a view showing only employee names and hire dates:
```sql
CREATE VIEW EmployeeSummary AS
SELECT firstName, lastName, hireDate
FROM Employees;
```

---

### 12. **ALTER TABLE (Modifications)**
#### a. **Adding a New Column**
To add a column for departmentID:
```sql
ALTER TABLE Employees
ADD departmentID INT;
```

#### b. **Dropping a Column**
To drop the `contactDetails` column:
```sql
ALTER TABLE Employees
DROP COLUMN contactDetails;
```

---

### 13. **Constraints**
#### a. **Adding a NOT NULL Constraint**
To ensure `mailID` cannot be NULL:
```sql
ALTER TABLE Employees
MODIFY mailID VARCHAR(100) NOT NULL;
```

#### b. **Adding a Unique Constraint**
To ensure that `mailID` is unique:
```sql
ALTER TABLE Employees
ADD CONSTRAINT unique_mailID UNIQUE (mailID);
```

---

### 14. **Normalization**
#### a. **First Normal Form (1NF)**
Ensure that each column in `Employees` contains atomic values (no repeating groups):
```sql
-- This is ensured in the `Employees` table by defining columns with single values.
```

#### b. **Second Normal Form (2NF)**
Ensure that all non-key columns are fully dependent on the primary key:
```sql
-- The `Employees` table satisfies 2NF as all columns depend on `employeeID`.
```

#### c. **Third Normal Form (3NF)**
Ensure that all non-key columns are not transitively dependent on the primary key:
```sql
-- The `Employees` table satisfies 3NF because there are no transitive dependencies.
```

---

### 15. **ACID Properties**
- **Atomicity**: Transactions are all-or-nothing (`COMMIT`/`ROLLBACK`).
- **Consistency**: The database transitions from one valid state to another.
- **Isolation**: Concurrent transactions do not affect each other.
- **Durability**: Once a transaction is committed, it is permanent.

---

These queries should help with your revision by covering essential SQL concepts using practical examples with the `Employees` table!
