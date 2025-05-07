Let's dive into **REST APIs (Representational State Transfer APIs)** in the context of **system design**—focusing on how they're used to architect scalable, maintainable, and loosely coupled systems.

---

## 🔍 What is a REST API?

A **REST API** is an **HTTP-based interface** that follows certain architectural principles to allow clients to access and manipulate resources in a standardized, stateless manner.

It’s widely used in **web and mobile applications**, microservices, and system integrations.

---

## 🧱 Key Concepts of REST in System Design

### 1. **Resource-Oriented Design**

* REST APIs expose **resources** (like `users`, `orders`, `products`) via **URLs**.
* Each resource is identified by a **URI** (Uniform Resource Identifier).

```
GET /users/123       → Fetch user with ID 123  
POST /orders         → Create a new order  
PUT /products/45     → Update product with ID 45  
DELETE /cart/99      → Remove cart item 99
```

---

### 2. **Statelessness**

* Each request from the client contains **all the information** the server needs to fulfill it.
* Server does **not store client context** between requests.

**Design implication**: APIs are **horizontally scalable**—any server instance can handle any request.

---

### 3. **HTTP Methods and Semantics**

| HTTP Method | Description             | Idempotent? | Safe? |
| ----------- | ----------------------- | ----------- | ----- |
| `GET`       | Read a resource         | ✅           | ✅     |
| `POST`      | Create a resource       | ❌           | ❌     |
| `PUT`       | Update/replace resource | ✅           | ❌     |
| `DELETE`    | Delete a resource       | ✅           | ❌     |
| `PATCH`     | Partially update        | ❌           | ❌     |

---

### 4. **HTTP Status Codes**

| Code | Meaning               | Usage Example            |
| ---- | --------------------- | ------------------------ |
| 200  | OK                    | Successful GET/PUT       |
| 201  | Created               | Successful POST          |
| 400  | Bad Request           | Invalid input            |
| 401  | Unauthorized          | Missing or invalid token |
| 404  | Not Found             | Resource doesn’t exist   |
| 500  | Internal Server Error | Unexpected server error  |

---

## 🛠 REST API in System Design Architecture

### 🔁 Typical Request Flow

```text
Client (Browser / Mobile App)
       ↓
API Gateway / Load Balancer
       ↓
Authentication Service (JWT/OAuth)
       ↓
RESTful Microservices (e.g., User, Product, Order)
       ↓
Database / External APIs
```

---

### 🧩 Benefits in System Design

| Feature              | System Design Advantage                                 |
| -------------------- | ------------------------------------------------------- |
| Statelessness        | Easy horizontal scaling                                 |
| Clear contract       | Loose coupling between services/components              |
| HTTP standardization | Widely supported, debug-friendly                        |
| Caching support      | Use of HTTP headers (`ETag`, `Cache-Control`) for speed |
| Monitoring/logging   | Built-in through HTTP layers and status codes           |

---

### 🔐 Authentication & Security

* Use **JWT tokens**, **OAuth**, or **API keys**.
* Secure endpoints with **HTTPS**.
* Use scopes and roles for fine-grained access control.

---

## 📈 REST in Microservices

REST is commonly used for **inter-service communication**, although for high performance internal communication, **gRPC** or **message queues** might be used instead.

```text
[ User Service ] ←→ [ Order Service ] ←→ [ Inventory Service ]
        (REST)           (REST)               (REST or gRPC)
```

To avoid tight coupling:

* Use **OpenAPI/Swagger** for documentation
* Enforce **API versioning** (`/v1/users`, `/v2/orders`)

---

## 🧪 Design Best Practices

* Use **plural nouns** for endpoints: `/users`, not `/getUser`
* Always return **appropriate status codes**
* Validate inputs and return **meaningful errors**
* Paginate large collections (`/users?page=2&limit=20`)
* Support **filtering** and **sorting**
* Document the API (OpenAPI, Swagger)

---

## 📦 Summary

| Concept        | Importance in System Design                     |
| -------------- | ----------------------------------------------- |
| Stateless      | Enables horizontal scaling and load balancing   |
| HTTP verbs     | Standardize CRUD operations                     |
| Resource-based | Promotes intuitive, modular architecture        |
| Status codes   | Improve monitoring and debugging                |
| Versioning     | Helps with backward compatibility and evolution |

---

