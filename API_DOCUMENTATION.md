# Customer API Documentation

## Base URL
`http://localhost:8080/api/customers`

---

## 1. Get All Customers

### **GET** `/api/customers`

Retrieve the full list of customers.

#### **Response: 200 OK**

```json
[
  {
    "id": 1,
    "customerCode": "C001",
    "fullName": "John Doe",
    "email": "john.doe@example.com"
  }
]
```

---

## 2. Get Customers with Pagination & Sorting

### **GET** `/api/customers?page=0&size=5&sortBy=fullName&sortDir=asc`

Supports:

* `page` (default: 0)
* `size` (default: 10)
* `sortBy` (any field)
* `sortDir` (`asc` | `desc`)

#### **Response: 200 OK**

```json
{
  "totalItems": 5,
  "totalPages": 1,
  "customers": [
    {
      "id": 4,
      "customerCode": "C004",
      "fullName": "Alice Brown",
      "email": "alice.brown@example.com",
      "phone": "+1-555-0104",
      "address": "321 Elm St, Houston, TX 77001",
      "status": "INACTIVE",
      "createdAt": "2025-12-06T14:01:21",
      "links": []
    },
    {
      "id": 3,
      "customerCode": "C003",
      "fullName": "Bob Johnson",
      "email": "bob.johnson@example.com",
      "phone": "+1-555-0103",
      "address": "789 Pine Rd, Chicago, IL 60601",
      "status": "ACTIVE",
      "createdAt": "2025-12-06T14:01:21",
      "links": []
    },
    {
      "id": 5,
      "customerCode": "C005",
      "fullName": "Charlie Wilson",
      "email": "charlie.wilson@example.com",
      "phone": "+1-555-0105",
      "address": "654 Maple Dr, Phoenix, AZ 85001",
      "status": "ACTIVE",
      "createdAt": "2025-12-06T14:01:21",
      "links": []
    },
    {
      "id": 2,
      "customerCode": "C002",
      "fullName": "Jane Smith",
      "email": "jane.smith@example.com",
      "phone": "+1-555-0102",
      "address": "456 Oak Ave, Los Angeles, CA 90001",
      "status": "ACTIVE",
      "createdAt": "2025-12-06T14:01:21",
      "links": []
    },
    {
      "id": 1,
      "customerCode": "C001",
      "fullName": "John Partially Updated",
      "email": "john.updated@example.com",
      "phone": "+1555999900",
      "address": "New Address",
      "status": "ACTIVE",
      "createdAt": "2025-12-06T14:01:21",
      "links": []
    }
  ],
  "currentPage": 0
}
```

---

## 3. Get Customer by ID

### **GET** `/api/customers/{id}`

#### **Response: 200 OK**

```json
{
  "id": 1,
  "customerCode": "C001",
  "fullName": "John Doe"
}
```

#### **Response: 404 Not Found**

```json
{
  "message": "Customer not found"
}
```

---

## 4. Create Customer

### **POST** `/api/customers`

#### **Request Body**

```json
{
  "customerCode": "C006",
  "fullName": "New Person",
  "email": "new.person@example.com",
  "phone": "+1-555-0106",
  "address": "100 River St",
  "status": "ACTIVE"
}
```

#### **Response: 201 Created**

```json
{
  "id": 6,
  "customerCode": "C006",
  "fullName": "New Person"
}
```

#### **Validation Error: 400 Bad Request**

```json
{
  "errors": {
    "email": "Invalid email format"
  }
}
```

---

## 5. Update Customer (Full Update)

### **PUT** `/api/customers/{id}`

#### **Request Body**

```json
{
  "fullName": "Updated Name",
  "email": "updated@example.com",
  "phone": "+123456789",
  "address": "Updated Address",
  "status": "ACTIVE"
}
```

#### **Response: 200 OK**

```json
{
  "message": "Customer updated successfully"
}
```

---

## 6. Partial Update Customer

### **PATCH** `/api/customers/{id}`

#### **Request Body**

```json
{ "fullName": "John Partially Updated" }
```

#### **Response: 200 OK**

```json
{
  "message": "Customer partially updated"
}
```

---

## 7. Delete Customer

### **DELETE** `/api/customers/{id}`

#### **Response: 200 OK**

```json
{
  "message": "Customer deleted successfully"
}
```

---

## 8. Search Customers

### **GET** `/api/customers/search?keyword=john`

#### **Response: 200 OK**

```json
[
  {
    "id": 1,
    "fullName": "John Doe"
  }
]
```

---

## 9. Filter by Status

### **GET** `/api/customers/status/{status}`

* `ACTIVE`
* `INACTIVE`

#### **Response: 200 OK**

```json
[
  {
    "id": 3,
    "fullName": "Bob Johnson",
    "status": "ACTIVE"
  }
]
```
