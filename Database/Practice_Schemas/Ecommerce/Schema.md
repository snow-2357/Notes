# Practice Schema: Ecommerce

## Tables

### 1. Users
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. Products
```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(12,2) NOT NULL, -- Never use FLOAT for money
    stock_quantity INT DEFAULT 0,
    category_id INT REFERENCES categories(id)
);
```

### 3. Orders
```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    status VARCHAR(50) DEFAULT 'pending', -- pending, paid, shipped, cancelled
    total_amount DECIMAL(12,2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 4. Order_Items (Junction Table)
```sql
CREATE TABLE order_items (
    order_id INT REFERENCES orders(id),
    product_id INT REFERENCES products(id),
    quantity INT NOT NULL,
    price_at_purchase DECIMAL(12,2) NOT NULL, -- Denormalized for audit
    PRIMARY KEY (order_id, product_id)
);
```

## Practice Queries

1.  **Revenue per Category:**
    ```sql
    SELECT c.name, SUM(oi.price_at_purchase * oi.quantity) as revenue
    FROM categories c
    JOIN products p ON p.category_id = c.id
    JOIN order_items oi ON oi.product_id = p.id
    GROUP BY c.name;
    ```

2.  **Top 5 Customers by Lifetime Value:**
    ```sql
    SELECT u.email, SUM(o.total_amount) as ltv
    FROM users u
    JOIN orders o ON o.user_id = u.id
    WHERE o.status = 'paid'
    GROUP BY u.email
    ORDER BY ltv DESC
    LIMIT 5;
    ```
