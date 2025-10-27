
# **Appendix: `sales_company` Database Schema & ERD**

## Part 1 — Text-Based Relational Schema

Below is the SQL-style schema extracted directly from the `sales_company` database.  
It lists all tables, their columns, data types, and key relationships.

### 1.1. DATABASE: sales_company

```
-- ============================================
-- TABLE: customers (16 rows)
-- ============================================
CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    country VARCHAR(50),
    signup_date DATE
);

-- ============================================
-- TABLE: products
-- ============================================
CREATE TABLE products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2),
    in_stock BOOLEAN
);

-- ============================================
-- TABLE: orders
-- ============================================
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- ============================================
-- TABLE: order_items
-- ============================================
CREATE TABLE order_items (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

### 1.2. Relationships Summary

```
customers ───────┐
                 ▼
               orders ───────┐
                              ▼
                          order_items ───► products

```

### 1.3. Row Counts (from INSERT statements)

```
| **Table** | **Approx. Rows** |
|:--|:--:|
| customers | 16 |
| orders | ~1,000+ |
| order_items | ~5,400+ |
| products | (sample set) |
```

---

## Part 2 — Visual ERD (Light Theme)
A clean, documentation-friendly diagram of the sales_company database, showing logical relationships among all tables.

---

## Part 3 — Visual ERD (Dark Theme)
A modern, presentation-ready dark theme version of the same diagram.

