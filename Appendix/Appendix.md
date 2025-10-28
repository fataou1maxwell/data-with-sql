
# **Appendix: `sales_company` Database Schema & ERD**

## Text-Based Relational Schema

Below is the SQL-style schema extracted directly from the `sales_company` database.  
It lists all tables, their columns, data types, and key relationships.

### 1. DATABASE: sales_company

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

### 2. Relationships Summary

```
customers ───────┐
                 ▼
               orders ───────┐
                              ▼
                          order_items ───► products

```

#### Interpretation Tip

- Customers connect to orders via customer_id
- Each order has multiple order_items
- Each order_item corresponds to a specific product


### 3. Row Counts (from INSERT statements)

```
| **Table**        | **Approx. Rows**    |
|------------------|---------------------|
| customers        | 16                  |
| orders           | ~1,000+             |
| order_items      | ~5,400+             |
| products         | (sample set)        |
```

##  Entity-Relationship Diagram (ERD)

The following Mermaid ERD shows how tables in the `sales_company` database relate to one another.  

```
    CUSTOMERS ||--o{ ORDERS : "places"
    ORDERS ||--|{ ORDER_ITEMS : "contains"
    PRODUCTS ||--o{ ORDER_ITEMS : "referenced in"

    CUSTOMERS {
        int customer_id PK
        varchar first_name
        varchar last_name
        varchar email
        varchar country
        date signup_date
    }

    ORDERS {
        int order_id PK
        int customer_id FK
        date order_date
    }

    ORDER_ITEMS {
        int order_item_id PK
        int order_id FK
        int product_id FK
        int quantity
    }

    PRODUCTS {
        int product_id PK
        varchar product_name
        varchar category
        decimal price
        boolean in_stock
    }
