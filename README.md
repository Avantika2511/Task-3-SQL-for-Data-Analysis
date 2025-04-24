SQL Data Analysis using MySQL
🧱 Step 1: Install MySQL
🔧 Download & Install:
Go to the MySQL Downloads Page
Download the MySQL Installer for your OS.
During installation, install:
MySQL Server
MySQL Workbench
Set a root password (to log in).

🗃 Step 2: Set Up Your Database
Open MySQL Workbench.
Run this in a new SQL tab:
Sql code:
CREATE DATABASE ecommerce;
USE ecommerce;

CREATE TABLE Customers (
  customer_id INT PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100)
);

CREATE TABLE Products (
  product_id INT PRIMARY KEY,
  name VARCHAR(100),
  category VARCHAR(50),
  price DECIMAL(10,2)
);
CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  order_date DATE,
  total_amount DECIMAL(10,2),
  FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);

CREATE TABLE Order_Items (
  order_item_id INT PRIMARY KEY,
  order_id INT,
  product_id INT,
  quantity INT,
  price DECIMAL(10,2),
  FOREIGN KEY (order_id) REFERENCES Orders(order_id),
  FOREIGN KEY (product_id) REFERENCES Products(product_id)
);

💾 Step 3: Insert Sample Data:
 insert data manually:
sql code:
INSERT INTO Customers VALUES (1, 'Alice', 'alice@gmail.com'); ..(like this more)
INSERT INTO Products VALUES (1, 'Laptop', 'Electronics', 999.99); ..(like this more)
INSERT INTO Orders VALUES (1, 1, '2024-01-01', 999.99); ..(like this more)
INSERT INTO Order_Items VALUES (1, 1, 1, 1, 999.99); ..(like this more)
🧠 Step 4: Write SQL Queries for Analysis
Use the MySQL Workbench to write your queries. Here's a sample set:
✅ a. Basic Query
Sql code:
SELECT name, email FROM CustomersWHERE name LIKE 'A%';
✅ b. JOIN + GROUP BY + Aggregates
Sql code
SELECT c.name, SUM(o.total_amount) AS total_spent
FROM Customers c
JOIN Orders o ON c.customer_id = o.customer_id
GROUP BY c.name;
✅ c. Subquery
Sql code:
SELECT name FROM Customers
WHERE customer_id IN (
  SELECT customer_id FROM Orders
  GROUP BY customer_id
  HAVING SUM(total_amount) > (
    SELECT AVG(total_amount) FROM Orders
  )
);
✅ d. Create a View
Sql code:
CREATE VIEW customer_summary AS
SELECT c.name, COUNT(o.order_id) AS total_orders, SUM(o.total_amount) AS total_spent
FROM Customers c
JOIN Orders o ON c.customer_id = o.customer_id
GROUP BY c.name;
📈 Step 5: Optimize with Indexes
sql code:
CREATE INDEX idx_customer_id ON Orders(customer_id);
CREATE INDEX idx_order_date ON Orders(order_date);

📸 Step 6: Document Results
Take screenshots of your queries + results in MySQL Workbench.
Save your queries in a .sql file (e.g., ecommerce_analysis.sql)
Create a PDF report with your screenshots.
