# Data Structures Visualization — Backend

A Spring Boot REST API that powers the Data Structures Visualization platform. The backend manages user authentication, data structure creation, operation execution, memory snapshot generation, and operation history. Each operation is executed step-by-step and produces intermediate memory snapshots that the frontend renders as interactive D3 visualizations.

> **This is the backend half of a full-stack project.** The frontend provides the interactive visualization interface, operation controls, snapshot playback, and PDF export functionality. This repository focuses on data structure implementations, operation execution, persistence, and API delivery.

---

## Features

* **11 data structure types** — Vector, Stack, Queue, Map, Set, Tree, Editor Buffer, Grid, Deque, Web Browser, Big Integer
* **Multiple implementations per type** — supports several underlying implementations for educational comparison and visualization
* **Memory snapshot generation** — every operation records intermediate execution states for step-by-step visualization
* **Operation history tracking** — complete history of executed operations with stored snapshots and results
* **Persistent storage** — all user-created data structures and histories are stored in PostgreSQL
* **JWT authentication** — secure login and registration using Spring Security and JWT
* **RESTful API design** — dedicated endpoints for creation, querying, and manipulation of each data structure type
* **Visualization-ready responses** — APIs return memory structures, heap objects, variables, and metadata optimized for frontend rendering
* **OpenAPI documentation** — Swagger UI integration for interactive API exploration
* **Spring Actuator support** — monitoring and runtime diagnostics endpoints

---

## Tech Stack

| Layer         | Technology              |
| ------------- | ----------------------- |
| Language      | Java 21                 |
| Framework     | Spring Boot 3.4         |
| Security      | Spring Security + JWT   |
| Persistence   | Spring Data JPA         |
| Database      | PostgreSQL              |
| Validation    | Jakarta Bean Validation |
| Documentation | OpenAPI / Swagger       |
| Monitoring    | Spring Boot Actuator    |
| Build         | Maven                   |

---

## Getting Started

### Prerequisites

* Java 21+
* Maven 3.9+
* PostgreSQL 14+

### Installation

```bash
git clone https://github.com/Xorxe7421/DataStructuresVisualizationBackend
cd DataStructuresVisualizationBackend
```

### Database Setup

Create a PostgreSQL database:

```sql
CREATE DATABASE data_structures_visualization;
```

### Configuration

Set the required environment variables:

```bash
export DB_URL=jdbc:postgresql://localhost:5432/data_structures_visualization
export DB_USERNAME=postgres
export DB_PASSWORD=password
```

Alternatively configure them in `application.yml`.

### Run

```bash
./mvnw spring-boot:run
```

The API starts at:

```text
http://localhost:8080
```

---

## API Documentation

Swagger UI is available after startup:

```text
http://localhost:8080/swagger-ui/index.html
```

OpenAPI documentation:

```text
http://localhost:8080/v3/api-docs
```

---

## Authentication

The API uses JWT-based authentication.

### Register

```http
POST /auth/register
```

### Login

```http
POST /auth/login
```

Successful authentication returns a JWT token which must be included in subsequent requests:

```http
Authorization: Bearer <token>
```

---

## Data Structures & Operations

| Type          | Implementations                                                                                                                       | Operations                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Vector        | Array, Linked List                                                                                                                    | add, get, set, insertAt, removeAt, size, isEmpty, clear                                                     |
| Stack         | Array, Linked List, Two-Queue                                                                                                         | push, pop, peek, size, isEmpty, clear                                                                       |
| Queue         | Array, Linked List, Unsorted Vector Priority, Sorted Linked List Priority, Unsorted Doubly Linked List Priority, Binary Heap Priority | enqueue, dequeue, peek, size, isEmpty, clear                                                                |
| Map           | Array, Hash                                                                                                                           | put, get, containsKey, size, isEmpty, clear                                                                 |
| Set           | Hash, Move-To-Front                                                                                                                   | add, remove, contains, size, isEmpty, clear                                                                 |
| Tree          | Binary Search Tree                                                                                                                    | insert, remove, search, clear                                                                               |
| Editor Buffer | Array, Two-Stack, Linked List, Doubly Linked List                                                                                     | insertCharacter, deleteCharacter, moveCursorForward, moveCursorBackward, moveCursorToStart, moveCursorToEnd |
| Grid          | Grid                                                                                                                                  | set, get, numRows, numColumns, inBounds                                                                     |
| Deque         | Deque                                                                                                                                 | pushFront, pushBack, popFront, popBack, getFront, getBack, size, isEmpty, clear                             |
| Web Browser   | Doubly Linked List                                                                                                                    | visit, forward, back                                                                                        |
| Big Integer   | Big Integer                                                                                                                           | add, isGreaterThan                                                                                          |

---

## Snapshot-Based Execution

The core feature of the backend is step-by-step execution recording.

For every operation:

1. The operation is executed incrementally.
2. Intermediate memory states are captured.
3. Variables and heap objects are serialized into snapshot models.
4. Snapshots are stored alongside operation history.
5. The frontend replays snapshots to visualize execution.

This allows users to observe how a data structure evolves internally rather than only viewing the final state.

---

## Memory Model

Snapshots contain visualization-oriented metadata, including:

* Local variables
* Instance variables
* Heap objects
* Object references
* Memory addresses
* Primitive values
* Operation results

This abstraction allows multiple data structure implementations to be rendered consistently by the frontend visualization engine.

---

## Main Endpoints

### User

```http
GET    /user/me
GET    /user/get-all-data-structures
DELETE /user/delete/{name}
```

### Stack

```http
POST /stack/create/{type}/{name}
GET  /stack/find/{type}/{name}
```

### Queue

```http
POST /queue/create/{type}/{name}
GET  /queue/find/{type}/{name}
```

### Vector

```http
POST /vector/create/{type}/{name}
GET  /vector/find/{type}/{name}
```

### Map

```http
POST /map/create/{type}/{name}
GET  /map/find/{type}/{name}
```

### Set

```http
POST /set/create/{type}/{name}
GET  /set/find/{type}/{name}
```

### Tree

```http
POST /tree/create/{type}/{name}
GET  /tree/find/{type}/{name}
```

### Grid

```http
POST /grid/create/{name}/{rows}/{columns}
GET  /grid/find/{name}
```

### Editor Buffer

```http
POST /editor-buffer/create/{type}/{name}
GET  /editor-buffer/find/{type}/{name}
```

### Deque

```http
POST /deque/create/{name}
GET  /deque/find/{name}
```

### Web Browser

```http
POST /web-browser/create/{name}
GET  /web-browser/find/{name}
```

### Big Integer

```http
POST /big-integer/create/{name}/{number}
GET  /big-integer/find/{name}
```

---

## Project Structure

```text
src/main/java/org/gpavl/datastructuresvisualizationbackend
│
├── controller/          # REST API endpoints
├── service/             # Business logic and operation execution
├── repository/          # Spring Data JPA repositories
├── entity/              # Persistent entities
├── model/               # Data structures, snapshots, DTOs
├── security/            # JWT authentication and authorization
├── exception/           # Exception handling
└── util/                # Shared utilities
```

---

## Monitoring

Spring Actuator endpoints are enabled for diagnostics and monitoring.

Example:

```http
GET /actuator/env
```

Additional endpoints can be enabled through Spring configuration.

---

## Development

Run tests:

```bash
./mvnw test
```

Build the project:

```bash
./mvnw clean package
```

Run the packaged JAR:

```bash
java -jar target/DataStructuresVisualizationBackend-0.0.1-SNAPSHOT.jar
```

---

## Author

**Giorgi Pavliashvili**
[LinkedIn](https://www.linkedin.com/in/giorgi-pavliashvili-6718861b6/)
