# 🍽️ Restaurant REST API

**Kantapon Hemmadhun — 6510545276**

A Spring Boot REST API for managing restaurant data, built as part of the lab for **Software Development Security (01219325)** at Kasetsart University.

---

## 📋 Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 25 |
| Framework | Spring Boot 4.1.1 |
| Web | Spring Web MVC |
| Persistence | Spring Data JPA + Hibernate |
| Database | H2 (in-memory) |
| Build Tool | Maven Wrapper (`mvnw`) |

---

## 🗂️ Project Structure

```
src/main/java/ku/restaurant/
├── RestaurantApplication.java     # Entry point
├── controller/
│   └── RestaurantController.java  # REST endpoints
├── entity/
│   └── Restaurant.java            # JPA entity
├── repository/                    # Spring Data repository
└── service/                       # Business logic layer

src/main/resources/
├── application.properties         # App configuration
├── .env                           # Local environment variables (git-ignored)
└── .env.example                   # Template for environment variables
```

---

## ⚙️ Setup & Configuration

### 1. Clone the repository

```bash
git clone <repository-url>
cd restaurant-api-2026
```

### 2. Configure environment variables

Copy the example env file and edit if needed:

```bash
cp src/main/resources/.env.example src/main/resources/.env
```

Default `.env` values (uses H2 in-memory database — no installation required):

```properties
SPRING_DATASOURCE_URL=jdbc:h2:mem:restaurant
SPRING_DATASOURCE_DRIVER=org.h2.Driver
SPRING_DATASOURCE_USERNAME=test
SPRING_DATASOURCE_PASSWORD=test
SPRING_JPA_HIBERNATE_DIALECT=org.hibernate.dialect.H2Dialect
```

### 3. Run the application

```bash
./mvnw spring-boot:run
```

The server starts on **http://localhost:8090**

---

## 🗄️ H2 Console

An embedded H2 web console is available for inspecting the in-memory database at runtime:

```
http://localhost:8090/h2-console/
```

| Field | Value |
|---|---|
| JDBC URL | `jdbc:h2:mem:restaurant` |
| Username | `test` |
| Password | `test` |

---

## 📦 Data Model — `Restaurant`

| Field | Type | Description |
|---|---|---|
| `id` | `int` | Auto-generated primary key |
| `name` | `String` | Restaurant name |
| `rating` | `double` | Rating score |
| `location` | `String` | Location / address |
| `createdAt` | `Instant` | Timestamp of creation |

---

## 🔌 API Endpoints

Base path: `/api`

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/restaurants` | Get all restaurants |
| `GET` | `/api/restaurants/{id}` | Get restaurant by ID |
| `GET` | `/api/restaurants/name/{name}` | Get restaurant by name |
| `GET` | `/api/restaurants/location/{location}` | Get restaurants by location |
| `POST` | `/api/restaurants` | Create a new restaurant |
| `PUT` | `/api/restaurants` | Update an existing restaurant |
| `DELETE` | `/api/restaurants/{id}` | Delete a restaurant by ID |

### Example — Create Restaurant

```bash
curl -X POST http://localhost:8090/api/restaurants \
  -H "Content-Type: application/json" \
  -d '{
    "name": "KU Canteen",
    "rating": 4.5,
    "location": "Kasetsart University, Bangkok",
    "createdAt": "2026-10-14T10:00:00Z"
  }'
```

### Example — Get All Restaurants

```bash
curl http://localhost:8090/api/restaurants
```

---

## 🧪 Running Tests

```bash
./mvnw test
```

---

## 📝 Notes

- The `.env` file is **git-ignored** — never commit credentials to version control.
- Use `.env.example` as the reference template for other developers.
- The H2 database is **in-memory only**; all data is lost when the application stops.
- `spring.jpa.hibernate.ddl-auto=update` auto-creates/updates the schema on startup.

