# Book-Store SQL — Example Queries

This file collects example SQL queries for the Book-Store-SQL project. You can add this file to the repo (suggested path: `sql/queries.md`) so others can quickly run and test common queries against the sample database.

## How to use
- Run these queries against your test database (SQLite / PostgreSQL / MySQL) after loading `sql/schema.sql` and `sql/seeds.sql`.
- Adjust table/column names if your schema differs.
- Date and currency literals may need minor syntax changes depending on your SQL engine.

---

## Basic Queries

-- 1) Retrieve all books in the "Fiction" genre:
```sql
SELECT * FROM BOOKS
WHERE GENRE = 'Fiction';
```

-- 2) Find books published after the year 1950:
```sql
SELECT * FROM BOOKS
WHERE PUBLISHED_YEAR > 1950;
```

-- 3) List all customers from Canada:
```sql
SELECT * FROM Customers
WHERE Country = 'Canada';
```

-- 4) Show orders placed in November 2023:
```sql
SELECT * FROM orders
WHERE order_date BETWEEN '2023-11-01' AND '2023-11-30';
```

-- 5) Retrieve the total stock of books available:
```sql
SELECT SUM(stock) AS total_stock FROM books;
```

-- 6) Find the details of the most expensive book:
```sql
SELECT * FROM books
ORDER BY price DESC
LIMIT 1;
```

-- 7) Show all orders with quantity greater than 1:
```sql
SELECT * FROM orders
WHERE quantity > 1;
```

-- 8) Retrieve all orders where the total amount exceeds $20:
```sql
SELECT * FROM orders
WHERE total_amount > 20;
```

-- 9) List all genres available in the Books table:
```sql
SELECT DISTINCT genre FROM books;
```

-- 10) Find the book with the lowest stock:
```sql
SELECT * FROM books
ORDER BY stock
LIMIT 1;
```

-- 11) Calculate the total revenue generated from all orders:
```sql
SELECT SUM(total_amount) AS Revenue
FROM orders;
```

---

## Advanced Queries

-- 1) Retrieve the total number of books sold for each genre:
```sql
SELECT b.genre, SUM(o.quantity) AS total_sold
FROM books b
JOIN orders o ON b.book_id = o.book_id
GROUP BY b.genre;
```

-- 2) Find the average price of books in the "Fantasy" genre:
```sql
SELECT AVG(price) AS avg_price
FROM books
WHERE genre = 'Fantasy';
```

-- 3) List customers who have placed at least 2 orders:
```sql
SELECT o.customer_id, c.name, COUNT(o.order_id) AS order_count
FROM orders o
JOIN customers c ON c.customer_id = o.customer_id
GROUP BY o.customer_id, c.name
HAVING COUNT(order_id) >= 2;
```

-- 4) Find the most frequently ordered book:
```sql
SELECT b.title, o.book_id, COUNT(o.order_id) AS Order_Ct
FROM orders o
JOIN books b ON o.book_id = b.book_id
GROUP BY b.title, o.book_id
ORDER BY Order_Ct DESC
LIMIT 1;
```

-- 5) Show the top 3 most expensive books of 'Fantasy' genre:
```sql
SELECT *
FROM books
WHERE genre = 'Fantasy'
ORDER BY price DESC
LIMIT 3;
```

-- 6) Retrieve the total quantity of books sold by each author:
```sql
SELECT b.author, SUM(o.quantity) AS total_quantity
FROM books b
JOIN orders o ON b.book_id = o.book_id
GROUP BY b.author;
```

-- 7) List the cities where customers who spent over $30 are located:
```sql
SELECT DISTINCT c.city
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE o.total_amount > 30;
```

-- 8) Find the customer who spent the most on orders:
```sql
SELECT c.customer_id, c.name, SUM(o.total_amount) AS Total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
ORDER BY Total_spent DESC
LIMIT 1;
```

-- 9) Calculate the stock remaining after fulfilling all orders:
```sql
SELECT b.book_id, b.title, b.stock,
       COALESCE(SUM(o.quantity), 0) AS Order_quantity,
       b.stock - COALESCE(SUM(o.quantity), 0) AS Remain_Qunt
FROM books b
LEFT JOIN orders o ON b.book_id = o.book_id
GROUP BY b.book_id, b.title, b.stock
ORDER BY b.book_id;
```

---

## Notes / Tips
- Use `EXPLAIN` or your DB's query planner to check performance on large datasets.
- Replace `LIMIT` with your DB-specific syntax if needed (e.g., `TOP` for some SQL Server versions).
- If your schema uses different column names or table names, update the queries accordingly.
- Consider adding index suggestions in `sql/README.md` if you plan to run these on larger data.
