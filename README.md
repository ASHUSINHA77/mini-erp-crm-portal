# 🚀 Mini ERP + CRM Operations Portal

<p align="center">
  <strong>A modern full-stack ERP & CRM platform for wholesale and distribution operations.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=white" />
  <img src="https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Node.js-20+-339933?style=for-the-badge&logo=node.js&logoColor=white" />
  <img src="https://img.shields.io/badge/Express.js-4-000000?style=for-the-badge&logo=express&logoColor=white" />
  <img src="https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
</p>

<p align="center">
  <a href="#-features">Features</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-tech-stack">Tech Stack</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-api">API</a>
</p>

---

## ✨ Overview

**Mini ERP + CRM Operations Portal** is a full-stack business management application designed for wholesale and distribution companies.

The platform brings together:

* 👥 Customer Relationship Management
* 📦 Product & Inventory Management
* 🔄 Stock Movement Tracking
* 🧾 Sales Challan Management
* 📊 Business Dashboard
* 🔐 JWT Authentication
* 🛡️ Role-Based Access Control
* 🗄️ PostgreSQL Database
* 🐳 Docker-based Local Infrastructure

The system follows a realistic business workflow:

```text
Customer Lead
     ↓
Follow-up
     ↓
Product & Stock Check
     ↓
Create Sales Challan
     ↓
Confirm Challan
     ↓
Stock Validation
     ↓
Stock Automatically Reduced
```

---

# 🎯 Key Features

## 🔐 Authentication & Authorization

* JWT-based authentication
* Secure password hashing using `bcryptjs`
* Role-based access control
* Protected API endpoints
* Four application roles:

| Role         | Responsibility              |
| ------------ | --------------------------- |
| 👑 Admin     | Full system access          |
| 💼 Sales     | Customers & sales challans  |
| 📦 Warehouse | Inventory & stock movements |
| 💰 Accounts  | Business/accounting access  |

---

## 👥 Customer CRM

Manage customer relationships from a centralized interface.

### Capabilities

* Create customers
* Search customers
* Track customer type
* Track customer status
* Store GST information
* Store business details
* Maintain follow-up dates
* Add customer notes
* Track follow-up activities

Supported customer types:

```text
Retail
Wholesale
Distributor
```

Customer lifecycle:

```text
Lead → Follow-up → Active
                  ↓
               Inactive
```

---

## 📦 Inventory Management

Manage products and monitor stock levels.

### Capabilities

* Add products
* Search inventory
* SKU management
* Product categorization
* Unit pricing
* Current stock tracking
* Minimum stock alerts
* Warehouse/location tracking
* Stock IN operations
* Stock OUT operations
* Stock movement history

Low-stock products are automatically highlighted when:

```text
Current Stock ≤ Minimum Stock Alert Quantity
```

---

## 🔄 Stock Movement Tracking

Every inventory adjustment is recorded.

Each stock movement contains:

```text
Product
Quantity
Movement Type
Reason
Created By
Timestamp
```

Supported movement types:

```text
IN
OUT
```

This provides an auditable inventory trail.

---

# 🧾 Sales Challans

Create and manage sales challans directly from the portal.

### Features

* Create draft challans
* Confirm challans
* Select customers
* Add multiple products
* Specify quantities
* Calculate total quantities
* Track challan status
* Store product snapshot information
* Automatically update inventory

### Challan lifecycle

```text
Draft
  │
  ├──────────────┐
  ↓              ↓
Confirmed     Cancelled
  │
  ↓
Stock Reduced
```

### 🛡️ Stock Safety

Confirmed challans use database-level transactional logic.

If requested quantity exceeds available stock:

```text
❌ Insufficient Stock
        ↓
409 Conflict
        ↓
Transaction Rejected
        ↓
Stock Remains Unchanged
```

This prevents negative inventory.

---

# 📊 Dashboard

The dashboard provides a quick overview of business operations.

### Metrics

* 👥 Total Customers
* 📦 Total Products
* 🧾 Confirmed Challans
* ⚠️ Low Stock Products

It also visualizes the primary business workflow:

```text
Lead
 ↓
Follow-up
 ↓
Stock Check
 ↓
Confirmed Challan
 ↓
Stock Reduced
```

---

# 🏗️ Architecture

```text
                    ┌──────────────────────┐
                    │      React UI        │
                    │   TypeScript + Vite  │
                    └──────────┬───────────┘
                               │
                               │ REST API
                               ↓
                    ┌──────────────────────┐
                    │   Express Backend    │
                    │   Node.js + TypeScript│
                    └──────────┬───────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ↓                ↓                ↓
          JWT Auth          Business Logic    Validation
              │                │                │
              └────────────────┼────────────────┘
                               ↓
                    ┌──────────────────────┐
                    │     PostgreSQL       │
                    │      Database        │
                    └──────────────────────┘

                         Docker Compose
```

---

# 🧰 Tech Stack

### Frontend

* React 18
* TypeScript
* Vite
* CSS
* Lucide React

### Backend

* Node.js
* Express.js
* TypeScript
* JWT
* bcryptjs
* Zod
* Helmet
* Morgan
* CORS

### Database

* PostgreSQL
* UUID-based identifiers
* Database constraints
* Transactions

### Infrastructure

* Docker
* Docker Compose
* npm Workspaces

---

# 📁 Project Structure

```text
mini-erp-crm-portal/
│
├── backend/
│   ├── src/
│   │   ├── server.ts
│   │   └── seed.ts
│   │
│   ├── schema.sql
│   ├── package.json
│   ├── tsconfig.json
│   └── .env.example
│
├── frontend/
│   ├── src/
│   │   ├── App.tsx
│   │   └── style.css
│   │
│   ├── index.html
│   ├── package.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   └── .env.example
│
├── docs/
│   └── postman_collection.json
│
├── docker-compose.yml
├── package.json
├── .gitignore
└── README.md
```

---

# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone https://github.com/ASHUSINHA77/mini-erp-crm-portal.git

cd mini-erp-crm-portal
```

---

## 2. Install Dependencies

```bash
npm install
```

This installs dependencies for both the frontend and backend workspaces.

---

## 3. Configure Environment Variables

### Backend

Create:

```text
backend/.env
```

Example:

```env
PORT=4000
DATABASE_URL=postgres://erp_user:erp_password@localhost:5432/mini_erp_crm
JWT_SECRET=change-this-secret
FRONTEND_ORIGIN=http://localhost:5173
```

### Frontend

Create:

```text
frontend/.env
```

Example:

```env
VITE_API_URL=http://localhost:4000
```

> ⚠️ Never commit `.env` files or production secrets to GitHub.

---

## 4. Start PostgreSQL

Using Docker Compose:

```bash
docker compose up -d
```

Verify the container:

```bash
docker compose ps
```

---

## 5. Seed the Database

```bash
npm run seed
```

This creates the initial users and sample business data.

---

## 6. Start the Application

```bash
npm run dev
```

The application will start on:

```text
Frontend → http://localhost:5173
Backend  → http://localhost:4000
```

---

# 🔑 Demo Accounts

All demo accounts use:

```text
Password: Password@123
```

| Role         | Email                   |
| ------------ | ----------------------- |
| 👑 Admin     | `admin@example.com`     |
| 💼 Sales     | `sales@example.com`     |
| 📦 Warehouse | `warehouse@example.com` |
| 💰 Accounts  | `accounts@example.com`  |

---

# 🌐 REST API

## Authentication

```http
POST /auth/login
```

---

## Dashboard

```http
GET /dashboard/summary
```

---

## Customers

```http
GET    /customers
POST   /customers
PUT    /customers/:id
POST   /customers/:id/followups
```

---

## Products

```http
GET    /products
POST   /products
PUT    /products/:id
POST   /products/:id/movements
GET    /products/movements/log
```

---

## Challans

```http
GET    /challans
POST   /challans
GET    /challans/:id
PATCH  /challans/:id/confirm
```

A Postman collection is included in:

```text
docs/postman_collection.json
```

---

# 🗄️ Database Design

The PostgreSQL database contains the following core entities:

```text
Users
  │
  ├── Customers
  │      └── Customer Follow-ups
  │
  ├── Products
  │      └── Stock Movements
  │
  └── Challans
         └── Challan Items
```

### Main Tables

| Table                | Purpose                    |
| -------------------- | -------------------------- |
| `users`              | Authentication & roles     |
| `customers`          | CRM customer records       |
| `customer_followups` | Customer follow-up history |
| `products`           | Product & inventory data   |
| `stock_movements`    | Inventory audit trail      |
| `challans`           | Sales challans             |
| `challan_items`      | Products inside challans   |

---

# 🛡️ Business Rules

The application implements important real-world business constraints.

### 1. No Negative Stock

```text
Available Stock = 10
Requested Stock = 15

Result → ❌ Transaction Rejected
```

### 2. Confirmed Challans Reduce Stock

```text
Stock Before = 100
Challan Quantity = 25

Stock After = 75
```

### 3. Database Transactions

Stock updates and challan confirmation are handled transactionally so that partial updates do not leave the system in an inconsistent state.

### 4. Product Snapshot

Challan items preserve:

```text
Product Name
SKU
Category
Unit Price
Quantity
Line Total
```

This means historical challans remain meaningful even if the product information changes later.

---

# 🔒 Security

The backend includes several security-focused practices:

* JWT authentication
* Password hashing with bcrypt
* Role-based authorization
* Helmet security middleware
* CORS configuration
* Request validation with Zod
* PostgreSQL constraints
* Transaction-safe stock updates
* Environment-based secrets

---

# 📈 Future Improvements

Potential production-level improvements include:

* [ ] Invoice PDF generation
* [ ] AWS deployment
* [ ] S3 document storage
* [ ] Advanced analytics
* [ ] Pagination and server-side filtering
* [ ] Automated email notifications
* [ ] Customer activity timeline
* [ ] Inventory reports
* [ ] Sales reports
* [ ] Audit log dashboard
* [ ] Automated testing
* [ ] CI/CD with GitHub Actions
* [ ] Production monitoring
* [ ] Redis caching

---

# 🧪 Build

Build both frontend and backend:

```bash
npm run build
```

Backend production build:

```bash
npm run build --workspace backend
```

Frontend production build:

```bash
npm run build --workspace frontend
```

---

# 🐳 Docker

Start the database:

```bash
docker compose up -d
```

Stop the database:

```bash
docker compose down
```

---

# 💡 Why This Project?

This project demonstrates practical full-stack engineering concepts including:

```text
React
   ↓
REST APIs
   ↓
Authentication
   ↓
Authorization
   ↓
Business Logic
   ↓
Database Transactions
   ↓
PostgreSQL
```

It is designed to demonstrate how a real business application can manage customers, products, inventory and sales operations through a single platform.

---

# 👨‍💻 Author

### Ashu Sinha

Software Engineering | Full-Stack Development | DSA

<p>
  <a href="https://github.com/ASHUSINHA77">
    <img src="https://img.shields.io/badge/GitHub-ASHUSINHA77-181717?style=for-the-badge&logo=github" />
  </a>
</p>

---

# ⭐ Support

If you found this project useful, consider giving the repository a ⭐ on GitHub.

---

<p align="center">
  <strong>Built with ❤️ using React, Node.js, TypeScript & PostgreSQL</strong>
</p>
