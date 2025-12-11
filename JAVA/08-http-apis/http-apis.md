# HTTP APIs — Quick Notes

## 1. What Is an API?
An **API (Application Programming Interface)** is a set of **endpoints** that you expose so other systems can interact with your application.

## 2. Endpoints and URIs
- **Endpoint = URI + HTTP method** (GET, POST, PUT, DELETE).  
- The **URI** points to a resource (e.g., `/users/1`).  
- The **HTTP method** defines the action (e.g., GET → fetch, POST → create).  
- Your **API = collection of endpoints**.
**Example**
    ```plaintext
    GET /api/v1/users  # This is an endpoint: Uri + HTTP method
    GET /api/v1/users/{id}
    POST /api/v1/users
    PUT /api/v1/users/{id}
    DELETE /api/v1/users/{id}
    ```

## 3. Resources vs Entities
- **Resource:** the business concept exposed by your API (shape tailored for clients).
- **Entity:** persistence model (DB/ORM).  
- Use DTOs to avoid leaking DB schema into the API.
  - **Entity** = database representation (all details, technical fields).
  - **DTO (Data Transfer Object)** = API representation (safe, controlled, stable contract).
  - it’s basically abstraction + encapsulation for data sharing.


## 4. Status Codes (use the right ones)
- **200** OK, **201** Created, **204** No Content  
- **400** Bad Request, **401** Unauthorized, **403** Forbidden  
- **404** Not Found, **409** Conflict, **422** Unprocessable Entity, **429** Too Many Requests  
- **500** Internal Server Error, **503** Service Unavailable


## 5. Implementation Details Don’t Matter to the Client
- Clients don’t care how your code works internally.  
- They only care that when they call an endpoint, they get the **expected response**.

## 6. Versioning (don’t break clients)
- Prefer **URI versioning**: `/api/v1/...`, `/api/v2/...`.
- Run **v1 and v2 side-by-side in the same deployment** (different controllers/routes).
- Deprecate with dates; provide migration notes and test both versions.


## 7. Documentation and Consistency
- Use documentation tools like **Swagger/OpenAPI** to describe your API.  
- The goal is to ensure others know:  
  - Which endpoints exist.  
  - What input they require.  
  - What output they return.  
- The key is **reliability and consistency**.

## 8. Interfaces Inside a Project
- Similarly, an **interface** in your code is like a contract between classes.  
- It defines what methods are available without specifying the implementation.  
- Just like an API lets external systems know what they can do, an interface lets different parts of your code interact cleanly.


## ✅ Takeaway
An **API** is just a **contract of endpoints**.  
Clients don’t need to know your implementation, only that those endpoints behave **as documented**.


---
# What is an API (General Concept)

- **API = Application Programming Interface**  
- It is a **generic concept**, not tied to web only.  
- An API is any **set of methods, classes, or endpoints** that allow one piece of software to interact with another.  
- The key idea: you **use the functionality** without worrying about how it is implemented internally.  

### Examples
- **JDBC API** → lets Java apps interact with relational databases.  
- **Java Collections API** → provides data structures like `List`, `Map`, etc.  
- **REST API** → exposes endpoints over HTTP (e.g., `/users`, `/orders`).  

👉 In all cases, **API = contract/interface** that defines *what* you can do, not *how* it works inside.  





