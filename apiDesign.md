# API Design - E-Commerce System

---

# 1. Overview

This document defines the REST API endpoints for the e-commerce system. The APIs follow REST principles, use JSON for data exchange, and support secure, scalable communication between client and server.

**Base URL:** `/api/v1`

---

# 2. Authentication

## 2.1 Login

**POST** `/auth/login`

### Request
{
  "email": "user@example.com",
  "password": "password123"
}

### Response
{
  "token": "jwt_token",
  "user_id": 101
}

### Status Codes
- 200 OK  
- 401 Unauthorized  

---

## 2.2 Register

**POST** `/auth/register`

### Request
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "phone": "9999999999"
}

### Response
{
  "user_id": 101,
  "message": "User registered successfully"
}

---

# 3. Product APIs

## 3.1 Get Products

**GET** `/products`

### Query Params
- search (optional)  
- category (optional)  
- min_price (optional)  
- max_price (optional)  
- page  
- limit  

### Response
{
  "products": [
    {
      "product_id": 1,
      "name": "iPhone 15",
      "price": 80000,
      "rating": 4.5
    }
  ],
  "total": 100
}

---

## 3.2 Get Product Details

**GET** `/products/{product_id}`

### Response
{
  "product_id": 1,
  "name": "iPhone 15",
  "description": "Latest iPhone",
  "price": 80000,
  "stock": 20
}

---

# 4. Cart APIs

## 4.1 Add to Cart

**POST** `/cart`

### Request
{
  "product_id": 1,
  "quantity": 2
}

### Response
{
  "message": "Item added to cart"
}

---

## 4.2 Get Cart

**GET** `/cart`

### Response
{
  "items": [
    {
      "product_id": 1,
      "quantity": 2
    }
  ],
  "total_price": 160000
}

---

## 4.3 Remove Item

**DELETE** `/cart/{product_id}`

---

# 5. Order APIs

## 5.1 Place Order

**POST** `/orders`

### Request
{
  "address_id": 10,
  "payment_method": "UPI"
}

### Response
{
  "order_id": 5001,
  "status": "PLACED"
}

---

## 5.2 Get Orders

**GET** `/orders`

### Response
{
  "orders": [
    {
      "order_id": 5001,
      "status": "DELIVERED",
      "total_amount": 160000
    }
  ]
}

---

## 5.3 Get Order Details

**GET** `/orders/{order_id}`

---

## 5.4 Cancel Order

**POST** `/orders/{order_id}/cancel`

---

# 6. Payment APIs

## 6.1 Initiate Payment

**POST** `/payments`

### Request
{
  "order_id": 5001,
  "payment_method": "CARD"
}

### Response
{
  "payment_id": 9001,
  "status": "SUCCESS"
}

---

# 7. Review APIs

## 7.1 Add Review

**POST** `/reviews`

### Request
{
  "product_id": 1,
  "rating": 5,
  "comment": "Excellent product"
}

---

## 7.2 Get Reviews

**GET** `/products/{product_id}/reviews`

---

# 8. Common Status Codes

- 200 OK – Success  
- 201 Created – Resource created  
- 400 Bad Request – Invalid input  
- 401 Unauthorized – Authentication required  
- 403 Forbidden – Access denied  
- 404 Not Found – Resource not found  
- 500 Internal Server Error – Server failure  

---

# 9. Design Considerations

## 9.1 RESTful Principles
- Use proper HTTP methods (GET, POST, DELETE)  
- Resource-based URLs  

## 9.2 Idempotency
- Order and payment APIs should prevent duplicate requests  

## 9.3 Pagination
- Required for product listing APIs  

## 9.4 Security
- JWT-based authentication  
- HTTPS required  

---