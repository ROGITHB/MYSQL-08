# E-Commerce Database System

This project is a simple **E-Commerce Database Management System** built using **MySQL**. The database is structured to manage customers, orders, and products efficiently. The database design follows **normalization principles**, ensuring data consistency and optimal performance.

## Database Overview

The system consists of three core tables:

- **Customers**: Stores customer information.
- **Orders**: Stores information about each order placed by customers.
- **Products**: Stores the product details.
- **Order_Items**: Normalized table to manage products within each order.
## Queries Included

1. **Retrieve all customers who have placed an order in the last 30 days**:
    ```sql
    SELECT * FROM customers 
    WHERE id IN (
        SELECT customer_id FROM orders 
        WHERE order_date >= CURDATE() - INTERVAL 30 DAY
    );
    ```

2. **Get the total amount of all orders placed by each customer**:
    ```sql
    SELECT customer_id, SUM(total_amount) AS total_spent 
    FROM orders 
    GROUP BY customer_id;
    ```

3. **Update the price of "Product C" to 45.00**:
    ```sql
    UPDATE products 
    SET price = 45.00 
    WHERE Products_name = 'Product C';
    ```

4. **Add a new column `discount` to the `products` table**:
    ```sql
    ALTER TABLE products 
    ADD COLUMN discount DECIMAL(5, 2) DEFAULT 0.00;
    ```

5. **Retrieve the top 3 products with the highest price**:
    ```sql
    SELECT * FROM products 
    ORDER BY price DESC 
    LIMIT 3;
    ```

6. **Get the names of customers who have ordered "Product A"**:
    ```sql
    SELECT c.name FROM customers c
    JOIN orders o ON c.id = o.customer_id
    JOIN order_items oi ON o.id = oi.order_id
    JOIN products p ON oi.product_id = p.id
    WHERE p.Products_name = 'Product A';
    ```

7. **Join the orders and customers tables to retrieve the customer's name and order date for each order**:
    ```sql
    SELECT c.name, o.order_date 
    FROM customers c 
    JOIN orders o ON c.id = o.customer_id;
    ```

8. **Retrieve the orders with a total amount greater than 150.00**:
    ```sql
    SELECT * FROM orders 
    WHERE total_amount > 150.00;
    ```

9. **Normalize the database by creating a separate table for order items**
    ```sql
     INSERT INTO order_items (order_id, product_id, quantity)
     VALUES(1, 1, 2),

10. **Retrieve the average total of all orders**:
    ```sql
    SELECT AVG(total_amount) AS average_order_total 
    FROM orders;
    ```
