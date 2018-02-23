# Databases

## CAP Theorem for Distributed Data Stores
- Consistency: every read receives the most recent write or throws an error.
- Availability: Every request receives a non-error response without guarantee that it contains the most recent write.
- Partition Tolerance: The system operates despite an arbitrary number of messages between nodes being dropped.

## ACID Database Transactions

- Atomicity: Transactions are all-or-nothing (either all operations occur or none occur - can't stop partway through).
- Consistency: Any transaction brings the database from one valid state to another (different from Consistency in CAP theorem).
- Isolation: Concureent executions of transactions has the same result as serially executing each transaction.
- Durability: Stored data is persistent.