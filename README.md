# Data Structures Visualization Backend

A Spring Boot backend application that powers a Data Structures Visualization platform. The system provides REST APIs for creating, managing, and visualizing various data structures while maintaining operation history, memory snapshots, and user-specific data.

## Features

### Authentication & User Management

* User registration and login
* JWT-based authentication and authorization
* User-specific data structure storage
* Secure API access using Spring Security

### Supported Data Structures

The backend provides APIs for working with:

* **Stack**
* **Queue**
* **Deque**
* **Vector**
* **Set**
* **Map**
* **Tree**
* **Grid**
* **Big Integer**
* **Editor Buffer**
* **Web Browser Simulation**

### Visualization Support

The application stores:

* Data structure states
* Operation history
* Memory snapshots
* Memory history

This enables frontend applications to visualize data structure operations step-by-step.

### Additional Features

* PostgreSQL persistence
* OpenAPI / Swagger documentation
* Bean validation
* Spring Actuator monitoring endpoints
* JPA/Hibernate data access

---

# Technology Stack

* Java 21
* Spring Boot 3.4
* Spring Security
* Spring Data JPA
* PostgreSQL
* JWT Authentication
* Spring Validation
* Spring Actuator
* OpenAPI (Swagger UI)
* Maven

---

# Project Structure

```text
src/main/java/org/gpavl/datastructuresvisualizationbackend

├── controller/        # REST API controllers
├── entity/            # Database entities
├── model/             # Data structure implementations and DTOs
├── repository/        # JPA repositories
├── security/          # JWT and security configuration
├── service/           # Business logic
├── exception/         # Global exception handling
└── util/              # Utility classes
```

---

# Prerequisites

Before running the application, ensure you have:

* Java 21+
* Maven 3.9+
* PostgreSQL database

---

# Environment Variables

The application requires the following environment variables:

| Variable      | Description               |
| ------------- | ------------------------- |
| `DB_URL`      | PostgreSQL connection URL |
| `DB_USERNAME` | Database username         |
| `DB_PASSWORD` | Database password         |

Example:

```bash
export DB_URL=jdbc:postgresql://localhost:5432/data_structures
export DB_USERNAME=postgres
export DB_PASSWORD=password
```

---

# Database Configuration

The application uses PostgreSQL and automatically updates the schema through Hibernate:

```yaml
spring:
  datasource:
    url: ${DB_URL}
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}

  jpa:
    hibernate:
      ddl-auto: update
```

Create a database before starting the application:

```sql
CREATE DATABASE data_structures;
```

---

# Running the Application

## Using Maven Wrapper

Linux / macOS:

```bash
./mvnw spring-boot:run
```

Windows:

```cmd
mvnw.cmd spring-boot:run
```

## Build the Project

```bash
./mvnw clean package
```

Run the generated JAR:

```bash
java -jar target/DataStructuresVisualizationBackend-0.0.1-SNAPSHOT.jar
```

---

# API Documentation

Once the application is running, Swagger/OpenAPI documentation will be available at:

```text
http://localhost:8080/swagger-ui.html
```

or

```text
http://localhost:8080/swagger-ui/index.html
```

---

# Main API Endpoints

## Authentication

```http
POST /auth/register
POST /auth/login
```

## User

```http
GET    /user/me
GET    /user/get-all-data-structures
DELETE /user/delete/{name}
```

## Stack

```http
POST /stack/create/{type}/{name}
GET  /stack/find/{type}/{name}
GET  /stack/size/{type}/{name}
GET  /stack/is-empty/{type}/{name}
GET  /stack/peek/{type}/{name}
```

## Queue

```http
POST /queue/create/{type}/{name}
GET  /queue/find/{type}/{name}
GET  /queue/size/{type}/{name}
GET  /queue/is-empty/{type}/{name}
GET  /queue/peek/{type}/{name}
```

## Deque

```http
POST /deque/create/{name}
GET  /deque/find/{name}
GET  /deque/get-front/{name}
GET  /deque/get-back/{name}
GET  /deque/size/{name}
GET  /deque/is-empty/{name}
```

## Vector

```http
POST /vector/create/{type}/{name}
GET  /vector/find/{type}/{name}
GET  /vector/get/{type}/{name}/{index}
GET  /vector/size/{type}/{name}
GET  /vector/is-empty/{type}/{name}
```

## Set

```http
POST /set/create/{type}/{name}
GET  /set/find/{type}/{name}
GET  /set/size/{type}/{name}
GET  /set/is-empty/{type}/{name}
```

## Map

```http
POST /map/create/{type}/{name}
GET  /map/find/{type}/{name}
GET  /map/get/{type}/{name}/{key}
GET  /map/contains-key/{type}/{name}/{key}
GET  /map/size/{type}/{name}
GET  /map/is-empty/{type}/{name}
```

## Tree

```http
POST /tree/create/{type}/{name}
GET  /tree/find/{type}/{name}
```

## Grid

```http
POST /grid/create/{name}/{rows}/{columns}
GET  /grid/find/{name}
GET  /grid/get/{name}/{row}/{column}
GET  /grid/in-bounds/{name}/{row}/{column}
GET  /grid/num-rows/{name}
GET  /grid/num-columns/{name}
```

## Big Integer

```http
POST /big-integer/create/{name}/{number}
GET  /big-integer/find/{name}
GET  /big-integer/is-greater-than/{name}/{number}
```

## Editor Buffer

```http
POST /editor-buffer/create/{type}/{name}
GET  /editor-buffer/find/{type}/{name}
```

## Web Browser

```http
POST /web-browser/create/{name}
GET  /web-browser/find/{name}
```

---

# Security

The application uses:

* JWT Authentication
* Spring Security
* Public/Private key signing

JWT keys are configured through:

```yaml
jwt:
  private:
    key: classpath:app.key
  public:
    key: classpath:app.pub
```

Ensure the required key files are available in the application resources.

---

# Monitoring

Spring Actuator is enabled.

Available endpoint:

```http
GET /actuator/env
```

---

# Development

To run tests:

```bash
./mvnw test
```

To package the application:

```bash
./mvnw clean package
```

---

# Future Improvements

* Additional data structure implementations
* Enhanced visualization metadata
* Real-time collaboration support
* Advanced operation replay system
* Performance analytics for algorithms
* Export/import visualization sessions

---

# License

This project is available for educational and learning purposes. Add your preferred license before production use.
