# Bảng Ghi Chú (Cheat Sheet) SQL cho Người Mới Bắt Đầu

Structured Query Language (SQL) là ngôn ngữ chuẩn để truy cập và thao tác cơ sở dữ liệu quan hệ. Bảng ghi chú này bao gồm những kiến thức cơ bản giúp bạn bắt đầu với SQL, kèm theo các ví dụ minh họa cho từng khái niệm.

---

## Mục Lục

1. [Các Lệnh SQL Cơ Bản](#1-các-lệnh-sql-cơ-bản)
2. [Lọc Dữ Liệu](#2-lọc-dữ-liệu)
3. [Sắp Xếp Dữ Liệu](#3-sắp-xếp-dữ-liệu)
4. [Hàm Tổng Hợp](#4-hàm-tổng-hợp)
5. [Nhóm Dữ Liệu](#5-nhóm-dữ-liệu)
6. [Kết Hợp Bảng (Joins)](#6-kết-hợp-bảng-joins)
7. [Subqueries](#7-subqueries)
8. [Thay Đổi Dữ Liệu](#8-thay-đổi-dữ-liệu)
9. [Tạo và Thay Đổi Bảng](#9-tạo-và-thay-đổi-bảng)
10. [Ràng Buộc (Constraints)](#10-ràng-buộc-constraints)
11. [Kiểu Dữ Liệu](#11-kiểu-dữ-liệu)

---

## 1. Các Lệnh SQL Cơ Bản

### SELECT

Truy xuất dữ liệu từ một hoặc nhiều bảng.

```sql
SELECT column1, column2, ...
FROM table_name;
```

**Ví dụ:**

```sql
SELECT first_name, last_name
FROM employees;
```

### FROM

Chỉ định bảng để truy xuất dữ liệu.

### WHERE

Lọc các bản ghi dựa trên điều kiện.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Ví dụ:**

```sql
SELECT *
FROM employees
WHERE department = 'Sales';
```

---

## 2. Lọc Dữ Liệu

### Toán Tử So Sánh

- `=` Bằng
- `<>` hoặc `!=` Khác
- `>` Lớn hơn
- `<` Nhỏ hơn
- `>=` Lớn hơn hoặc bằng
- `<=` Nhỏ hơn hoặc bằng

**Ví dụ:**

```sql
SELECT *
FROM products
WHERE price > 100;
```

### Toán Tử Logic

- `AND` Tất cả điều kiện phải đúng
- `OR` Ít nhất một điều kiện đúng
- `NOT` Đảo ngược giá trị đúng/sai

**Ví dụ:**

```sql
SELECT *
FROM employees
WHERE department = 'IT' AND salary > 50000;
```

### BETWEEN

Chọn các giá trị trong một khoảng.

```sql
SELECT *
FROM products
WHERE price BETWEEN 50 AND 100;
```

### IN

Kiểm tra giá trị có trong một tập hợp.

```sql
SELECT *
FROM employees
WHERE department IN ('HR', 'Finance', 'IT');
```

### LIKE

Tìm kiếm theo mẫu.

- `%` Đại diện cho không hoặc nhiều ký tự
- `_` Đại diện cho một ký tự

**Ví dụ:**

```sql
SELECT *
FROM customers
WHERE last_name LIKE 'Sm%';
```

---

## 3. Sắp Xếp Dữ Liệu

### ORDER BY

Sắp xếp kết quả theo thứ tự tăng dần (`ASC`) hoặc giảm dần (`DESC`).

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;
```

**Ví dụ:**

```sql
SELECT first_name, last_name
FROM employees
ORDER BY last_name ASC, first_name DESC;
```

---

## 4. Hàm Tổng Hợp

- `COUNT()` Trả về số lượng hàng
- `SUM()` Tổng cộng
- `AVG()` Giá trị trung bình
- `MIN()` Giá trị nhỏ nhất
- `MAX()` Giá trị lớn nhất

**Ví dụ:**

```sql
SELECT COUNT(*) AS total_employees
FROM employees;

SELECT AVG(salary) AS average_salary
FROM employees;
```

---

## 5. Nhóm Dữ Liệu

### GROUP BY

Nhóm các hàng có cùng giá trị trong các cột được chỉ định.

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;
```

**Ví dụ:**

```sql
SELECT department, COUNT(*) AS num_employees
FROM employees
GROUP BY department;
```

### HAVING

Lọc các nhóm dựa trên hàm tổng hợp.

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```

**Ví dụ:**

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

## 6. Kết Hợp Bảng (Joins)

### INNER JOIN

Trả về các bản ghi có giá trị khớp trong cả hai bảng.

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

**Ví dụ:**

```sql
SELECT employees.first_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

### LEFT JOIN

Trả về tất cả các bản ghi từ bảng bên trái và các bản ghi khớp từ bảng bên phải.

```sql
SELECT *
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

### RIGHT JOIN

Trả về tất cả các bản ghi từ bảng bên phải và các bản ghi khớp từ bảng bên trái.

### FULL OUTER JOIN

Trả về tất cả các bản ghi khi có sự khớp trong bảng bên trái hoặc bên phải.

---

## 7. Subqueries

Một truy vấn bên trong một truy vấn SQL khác.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name OPERATOR (SELECT column_name FROM table_name WHERE condition);
```

**Ví dụ:**

```sql
SELECT first_name, last_name
FROM employees
WHERE department_id IN (SELECT id FROM departments WHERE location = 'New York');
```

---

## 8. Thay Đổi Dữ Liệu

### INSERT INTO

Thêm các hàng mới vào bảng.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

**Ví dụ:**

```sql
INSERT INTO employees (first_name, last_name, department)
VALUES ('John', 'Doe', 'Marketing');
```

### UPDATE

Chỉnh sửa dữ liệu hiện có.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Ví dụ:**

```sql
UPDATE employees
SET salary = salary * 1.05
WHERE performance_rating = 'Excellent';
```

### DELETE

Xóa các hàng khỏi bảng.

```sql
DELETE FROM table_name
WHERE condition;
```

**Ví dụ:**

```sql
DELETE FROM employees
WHERE termination_date IS NOT NULL;
```

---

## 9. Tạo và Thay Đổi Bảng

### CREATE TABLE

Tạo một bảng mới.

```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);
```

**Ví dụ:**

```sql
CREATE TABLE departments (
    id INT PRIMARY KEY,
    department_name VARCHAR(50) NOT NULL
);
```

### ALTER TABLE

Thêm, sửa đổi hoặc xóa cột và ràng buộc.

- Thêm một cột:

  ```sql
  ALTER TABLE table_name
  ADD column_name datatype;
  ```

- Sửa đổi một cột:

  ```sql
  ALTER TABLE table_name
  MODIFY COLUMN column_name datatype;
  ```

- Xóa một cột:

  ```sql
  ALTER TABLE table_name
  DROP COLUMN column_name;
  ```

### DROP TABLE

Xóa một bảng và dữ liệu của nó.

```sql
DROP TABLE table_name;
```

---

## 10. Ràng Buộc (Constraints)

### PRIMARY KEY

Xác định duy nhất mỗi bản ghi.

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```

### FOREIGN KEY

Đảm bảo tính toàn vẹn tham chiếu giữa các bảng.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

### UNIQUE

Đảm bảo tất cả các giá trị trong một cột là duy nhất.

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

### NOT NULL

Đảm bảo một cột không thể có giá trị NULL.

### CHECK

Đảm bảo tất cả các giá trị thỏa mãn một điều kiện.

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    salary DECIMAL(10, 2),
    CHECK (salary >= 0)
);
```

---

## 11. Kiểu Dữ Liệu

- `INT` Số nguyên
- `DECIMAL(p,s)` Số thập phân với độ chính xác `p` và tỷ lệ `s`
- `VARCHAR(n)` Chuỗi ký tự có độ dài biến đổi lên đến `n` ký tự
- `CHAR(n)` Chuỗi ký tự cố định `n` ký tự
- `DATE` Ngày (YYYY-MM-DD)
- `TIME` Thời gian (HH:MI:SS)
- `DATETIME` Ngày và thời gian
- `BOOLEAN` Đúng hoặc sai

---

## Mẹo Bổ Sung

- **Đặt Biệt Danh (Aliasing) Cho Cột và Bảng:**

  ```sql
  SELECT column_name AS alias_name
  FROM table_name AS alias_name;
  ```

  **Ví dụ:**

  ```sql
  SELECT e.first_name, e.last_name, d.department_name
  FROM employees AS e
  INNER JOIN departments AS d
  ON e.department_id = d.id;
  ```

- **Ghi Chú Trong SQL:**

  - Ghi chú một dòng: `-- nội dung ghi chú`
  - Ghi chú nhiều dòng: `/* nội dung ghi chú */`

- **Nối Chuỗi:**

  - Sử dụng hàm `CONCAT()`:

    ```sql
    SELECT CONCAT(first_name, ' ', last_name) AS full_name
    FROM employees;
    ```

---

Hãy luôn nhớ sử dụng mệnh đề `WHERE` với các lệnh `UPDATE` và `DELETE` để tránh vô tình thay đổi hoặc xóa tất cả các bản ghi.
