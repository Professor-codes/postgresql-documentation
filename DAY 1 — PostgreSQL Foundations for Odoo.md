
## 1️⃣ What Is Data?

### Simple Explanation

- **Data** = raw information  
- Examples:
- Customer name
- Invoice amount
- Product price

### In Odoo Terms

- Customer name → `res.partner.name`
- Invoice total → `account.move.amount_total`

### Problem Without a Database

- Data scattered in files
- No relationships
- No safety
- No multi-user access

👉 **Odoo cannot exist without a database**

## 2️⃣ What Is a Database?

### Database = Organized Storage + Rules

A database:

- Stores data in **tables**
- Enforces **rules**
- Handles **multiple users at the same time**
- Prevents corruption

### Think of a Database Like This:

- Excel ❌ (single user, unsafe)
- Database ✅ (multi-user, safe, fast)

## 3️⃣ Tables, Rows, Columns

### Table

- Like an Excel sheet
- Example: `res_partner`

### Column

- Type of data
- Example:
- `id`
- `name`
- `email`

### Row

- One record
- One customer
- One invoice

### Odoo Example

|id|name|email|
|---|---|---|
|7|ABC Corp|abc@email.com|

- This row = one partner in Odoo UI

## 4️⃣ Relational Databases

### Relational Means:

- Tables are **connected to each other**
- Using **IDs (relationships)**

### Example

- Customer table
- Invoice table
- Invoice has `partner_id`

👉 Odoo is **100% relational**

## 5️⃣ Why PostgreSQL Specifically

### PostgreSQL Strengths

- Strong data consistency (ACID)
- Advanced indexing
- JSONB support
- Excellent concurrency handling
- Open-source & battle-tested

### Odoo Decision

- Odoo officially supports **ONLY PostgreSQL**
- No MySQL
- No MariaDB
- No SQLite

### Production Reality

> If PostgreSQL is slow or broken, **Odoo is slow or broken**

## 6️⃣ PostgreSQL vs Odoo

### PostgreSQL Responsibilities

- Store data
- Enforce constraints
- Optimize queries
- Handle locks & concurrency

### Odoo Responsibilities

- Business logic
- Access rules
- UI
- ORM

👉 **Odoo does NOT protect you from bad database decisions**

## 7️⃣ Odoo ORM — First Concept

### ORM = Object Relational Mapping

Simple meaning:

- Python objects ↔ Database rows

Example:

- Python: `partner.name = "ABC"`
- Database: `res_partner.name = 'ABC'`

### Why This Matters

- ORM auto-generates SQL
- Bad ORM usage = bad SQL
- PostgreSQL must still execute everything

## 8️⃣ One Odoo Database = One PostgreSQL Database

### Important Concept

- Each Odoo instance can have:
- Multiple databases
- Each database:
- Independent
- Separate data

### Example

- `odoo_prod`
- `odoo_test`
- `odoo_dev`

👉 **Never test in production database**

## 9️⃣ PostgreSQL Server vs Database vs Table

### PostgreSQL Server

- Running service
- Manages everything

### Database

- One Odoo instance data

### Table

- One Odoo model

Hierarchy:
```
PostgreSQL Server
 ├── odoo_prod (database)
 │    ├── res_partner (table)
 │    ├── sale_order
 │    └── account_move
 └── odoo_test
```