# Software Requirements Specification (SRS)
# E-Commerce Management DBMS Project

**Course:** Database Management Systems (DBMS) - ITE1003  
**Department:** Information Technology  
**Project Type:** Academic Database Project  

---

## 1. Introduction

### 1.1 Purpose

This Software Requirements Specification (SRS) document describes the requirements for the E-Commerce Management DBMS Project. The system is a SQL-based database management system designed to support an online clothing e-commerce platform. It enables sellers to list products, customers to browse and purchase items, and administrators to monitor sales and manage operations. The primary objective is to design a normalized relational database that fulfills all functional requirements of an e-commerce website.

### 1.2 Scope

The system provides the following capabilities:
- User registration and authentication for customers and sellers
- Product catalog management (add, view, filter products)
- Shopping cart functionality (add, remove, view cart items)
- Order processing and payment tracking
- Administrative features for monitoring sales, profits, and user activity
- PL/SQL functions and triggers for automated operations

The system is implemented using Oracle SQL Server and is intended for academic demonstration purposes.

### 1.3 Intended Audience

- **Students/Faculty:** For understanding database design and implementation
- **Developers:** As a reference for e-commerce database schema design
- **Administrators:** To understand data management and reporting capabilities

### 1.4 Definitions, Acronyms, and Abbreviations

| Term | Definition |
|------|------------|
| SRS | Software Requirements Specification |
| DBMS | Database Management System |
| ER Diagram | Entity-Relationship Diagram |
| PL/SQL | Procedural Language/Structured Query Language |
| SQL | Structured Query Language |
| Admin | Administrator of the system |
| Seller | A user who sells products |
| Customer | A user who purchases products |

---

## 2. Overall Description

### 2.1 Product Perspective

This project is a standalone database system designed as part of the DBMS course curriculum. It simulates the backend database of a real-world e-commerce platform. The system interacts with users through SQL queries and is intended to be integrated with a front-end application in the future.

### 2.2 Product Functions

1. **User Management:** Register, authenticate, and manage customer and seller accounts.
2. **Product Management:** Add, update, and delete products in the catalog.
3. **Cart Management:** Allow customers to add/remove products from their cart.
4. **Order & Payment:** Record transactions and track payment history.
5. **Admin Reporting:** Generate reports on sales, profits, and customer activity.
6. **Automated Operations:** Use PL/SQL triggers and procedures for data integrity.

### 2.3 User Classes and Characteristics

| User Class | Description |
|------------|-------------|
| Customer | End-user who browses products, adds to cart, and makes purchases |
| Seller | Vendor who lists products for sale and manages their inventory |
| Admin | System administrator who monitors overall platform activity and generates reports |

### 2.4 Operating Environment

- **Database:** Oracle SQL Server / Oracle Community Edition
- **Platform:** Web-based (designed for browser access)
- **Operating System:** Windows / Linux

### 2.5 Constraints

- Database must be implemented using Oracle SQL syntax
- All tables must follow normalization principles (at least 3NF)
- Data types and constraints must match Oracle SQL standards
- The system is for academic purposes and does not include real payment gateway integration

---

## 3. Specific Requirements

### 3.1 Functional Requirements

| ID | Requirement | Description |
|----|-------------|-------------|
| FR-01 | User Registration | A new user (customer or seller) can register on the website |
| FR-02 | View Cart | A customer can view details of products present in their cart |
| FR-03 | Order History | A customer can view their purchase/order history |
| FR-04 | Admin Sale Management | Admin can initiate sales with discounts on products |
| FR-05 | Product Filtering | Customers can filter products by size, gender, type, color, etc. |
| FR-06 | Cart Management | Customers can add or delete products from their cart |
| FR-07 | Seller Unregister | A seller can unregister or stop selling their products |
| FR-08 | Profile Update | Sellers and customers can update their personal details |
| FR-09 | Sales Report by Date | Admin can view products purchased on a particular date |
| FR-10 | Sales Count by Date | Admin can view the number of products sold on a particular date |
| FR-11 | Cart Total | Customer can view the total price of products in the cart |
| FR-12 | Inactive Customers | Admin can view customers who have not made any purchases |
| FR-13 | Profit Calculation | Admin can view total profit earned from website sales |

### 3.2 Database Schema

#### 3.2.1 Tables

| Table | Primary Key | Description |
|-------|-------------|-------------|
| Cart | Cart_id | Stores shopping cart information |
| Customer | Customer_id | Stores customer details and references cart |
| Seller | Seller_id | Stores seller account information |
| Seller_Phone_num | (Phone_num, Seller_id) | Stores multiple phone numbers per seller |
| Payment | payment_id | Records payment transactions |
| Product | Product_id | Stores product catalog details |
| Cart_item | (Cart_id, Product_id) | Links products to carts with quantity |

#### 3.2.2 Entity Relationships

- One Customer has One Cart (1:1)
- One Cart contains Many Cart_items (1:M)
- One Product can be in Many Cart_items (1:M)
- One Seller can list Many Products (1:M)
- One Customer can make Many Payments (1:M)
- One Seller can have Many Phone numbers (1:M)

### 3.3 Non-Functional Requirements

| ID | Requirement | Description |
|----|-------------|-------------|
| NFR-01 | Performance | Queries should execute within acceptable time limits (< 2 seconds) |
| NFR-02 | Data Integrity | Foreign key constraints must ensure referential integrity |
| NFR-03 | Security | Passwords should be stored securely (hashed) |
| NFR-04 | Scalability | Database should support growth in products and users |
| NFR-05 | Availability | System should be accessible during business hours |

---

## 4. System Features

### 4.1 Customer Features
- Browse and search product catalog
- Filter products by type, size, gender, color
- Add/remove items from shopping cart
- View cart total before checkout
- View order/purchase history
- Update personal profile

### 4.2 Seller Features
- Register as a seller
- List products for sale
- Update product details
- Unregister/stop selling
- Update seller profile

### 4.3 Admin Features
- View all products purchased on a specific date
- View count of products sold per date
- View total profit from sales
- Identify inactive customers (no purchases)
- Initiate promotional sales with discounts

---

## 5. External Interface Requirements

### 5.1 User Interfaces

The system is designed to be integrated with a web-based front-end interface. The database layer handles all data operations through SQL queries executed via the Oracle SQL console.

### 5.2 Database Interfaces

- Oracle SQL Server for data storage and retrieval
- PL/SQL for stored procedures and triggers
- Standard SQL for CRUD operations

---

## 6. PL/SQL Components

### 6.1 Stored Procedures

**cost_filter(c IN NUMBER, t IN VARCHAR)**
- Returns product types with cost less than the given threshold
- Uses cursor to iterate through matching products

### 6.2 Triggers

**before_pay_up (BEFORE INSERT ON Payment)**
- Automatically calculates total cost for a cart
- Updates the total_amount field in the Payment table
- Ensures accurate transaction recording

---

## 7. Appendix

### 7.1 SQL Commands Reference

All SQL commands for table creation, data insertion, and queries are provided in the main README.md file of this repository.

### 7.2 References

1. Oracle SQL Documentation
2. IEEE Standard for Software Requirements Specifications (IEEE Std 830-1998)
3. Database Management Systems - Course Material ITE1003

---

**Document Prepared By:** Utkarsh Anand  
**Date:** April 2026  
**Version:** 1.0
