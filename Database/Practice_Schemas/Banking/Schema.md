# Practice Schema: Banking Ledger

Banking requires 100% data integrity and strict normalization.

## Tables

### 1. Accounts
```sql
CREATE TABLE accounts (
    id UUID PRIMARY KEY,
    user_id INT NOT NULL,
    account_number VARCHAR(20) UNIQUE NOT NULL,
    balance DECIMAL(15, 2) DEFAULT 0.00,
    currency VARCHAR(3) DEFAULT 'USD',
    status VARCHAR(10) DEFAULT 'active', -- active, frozen, closed
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. Transactions
```sql
CREATE TABLE transactions (
    id UUID PRIMARY KEY,
    from_account_id UUID REFERENCES accounts(id),
    to_account_id UUID REFERENCES accounts(id),
    amount DECIMAL(15, 2) NOT NULL,
    type VARCHAR(20), -- transfer, deposit, withdrawal
    status VARCHAR(20), -- pending, completed, failed
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Critical Challenges & Queries

### 1. The Atomicity Test (A Transfer)
A transfer must be atomic. Both updates and the log entry must succeed or all must fail.
```sql
BEGIN;
-- Subtract from sender
UPDATE accounts SET balance = balance - 100 WHERE id = 'sender_uuid' AND balance >= 100;
-- Add to receiver
UPDATE accounts SET balance = balance + 100 WHERE id = 'receiver_uuid';
-- Log the transaction
INSERT INTO transactions (id, from_account_id, to_account_id, amount, type) 
VALUES (gen_random_uuid(), 'sender_uuid', 'receiver_uuid', 100, 'transfer');
COMMIT;
```

### 2. Audit Trail Query
"Show me the balance history for an account based on transactions."
```sql
SELECT 
    created_at,
    type,
    amount,
    SUM(CASE WHEN to_account_id = 'my_uuid' THEN amount ELSE -amount END) 
        OVER (ORDER BY created_at) as running_balance
FROM transactions
WHERE from_account_id = 'my_uuid' OR to_account_id = 'my_uuid';
```

## Security Rule
- Use **Row-Level Security (RLS)** to ensure `user_A` can never see `user_B`'s account data even if they find a way to run a query.
- Use **Check Constraints** to prevent balances from ever going negative (unless it's a credit account).
    - `ALTER TABLE accounts ADD CONSTRAINT positive_balance CHECK (balance >= 0);`
