# 🚀 Full-Stack E-Commerce App with Java Spring Boot and MySQL

## 📁 Repository: `Full-Stack-E-Commerce-App-with-Java-Spring-Boot-and-MySQL`

Welcome to the GitHub repository for the **Full-Stack E-Commerce Application** built using **Java Spring Boot** for the backend and **MySQL** for data storage. This README covers the Phase 1 development, which includes backend setup, REST API creation, and CRUD functionalities.

---

## 💡 Project Overview
This project is designed to demonstrate key industry-standard backend features such as:
- CRUD Operations
- RESTful API Design
- Database Integration (MySQL)
- Role-Based Backend with Product Management

Tech Stack:
- **Java 17**
- **Spring Boot 3.1+**
- **MySQL**
- **Spring Data JPA**
- **Lombok**
- **Postman (for API testing)**

---

## 🏗️ Phase 1: Backend Setup

### ✅ 1. Initialize Spring Boot Project
Use [Spring Initializr](https://start.spring.io/) to generate the base project with the following dependencies:
- Spring Web
- Spring Data JPA
- MySQL Driver
- Lombok
- DevTools

### ✅ 2. MySQL Configuration
```sql
CREATE DATABASE ecommerce_db;
```
Update `application.properties` with:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce_db
spring.datasource.username=root
spring.datasource.password=your-password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

server.port=8080

```

### ✅ 3. Create Product Entity
```java
package com.abhi.ecommerce.model;

import jakarta.persistence.*;

@Entity
@Table(name = "products")
public class product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String description;
    private double price;
    private String imageUrl;

    // ✅ Constructors
    public product() {
    }

    public product(String name, String description, double price, String imageUrl) {
        this.name = name;
        this.description = description;
        this.price = price;
        this.imageUrl = imageUrl;
    }

    // ✅ Getters and Setters
    public Long getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public String getImageUrl() {
        return imageUrl;
    }

    public void setImageUrl(String imageUrl) {
        this.imageUrl = imageUrl;
    }
}

```

### ✅ 4. Create Repository Interface
```java
package com.abhi.ecommerce.repository;

import com.abhi.ecommerce.model.product;
import org.springframework.data.jpa.repository.JpaRepository;

public interface repository extends JpaRepository<product, Long> {
}
```

### ✅ 5. Create REST API Controller
```java
package com.abhi.ecommerce.controller;

import com.abhi.ecommerce.model.product;
import com.abhi.ecommerce.repository.repository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;
import java.util.Optional;

@RestController
@RequestMapping("/api/products")
@CrossOrigin(origins = "*") // To allow frontend (React) calls
public class controller {

    @Autowired
    private repository productRepository;

    // ✅ GET all products
    @GetMapping
    public List<product> getAllProducts() {
        return productRepository.findAll();
    }

    // ✅ GET product by ID
    @GetMapping("/{id}")
    public Optional<product> getProductById(@PathVariable Long id) {
        return productRepository.findById(id);
    }

    // ✅ CREATE product
    @PostMapping
    public product createProduct(@RequestBody product product) {
        return productRepository.save(product);
    }

    // ✅ UPDATE product
    @PutMapping("/{id}")
    public product updateProduct(@PathVariable Long id, @RequestBody product updatedProduct) {
        product existingProduct = productRepository.findById(id)
                .orElseThrow(() -> new RuntimeException("Product not found with id " + id));

        existingProduct.setName(updatedProduct.getName());
        existingProduct.setDescription(updatedProduct.getDescription());
        existingProduct.setPrice(updatedProduct.getPrice());
        existingProduct.setImageUrl(updatedProduct.getImageUrl());

        return productRepository.save(existingProduct);
    }

    // ✅ DELETE product
    @DeleteMapping("/{id}")
    public String deleteProduct(@PathVariable Long id) {
        productRepository.deleteById(id);
        return "Product with ID " + id + " deleted successfully.";
    }
}
```

---

## 🧪 API Testing (Postman)
| Method | Endpoint | Description           |
|--------|----------|-----------------------|
| GET    | /api/products     | Retrieve all products       |
| POST   | /api/products     | Add a new product           |
| PUT    | /api/products/{id}| Update an existing product  |
| DELETE | /api/products/{id}| Delete a product by ID      |

---

## 🎯 Outcomes & Learnings
- Created and structured a Spring Boot backend
- Connected to MySQL for data persistence
- Implemented complete CRUD via REST APIs
- Tested endpoints using Postman


---

## 📎 Connect with Me
- LinkedIn: [(https://www.linkedin.com/in/nikam-rahul/)]


> 🌟 Star the repo if you find it helpful.
