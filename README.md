# 🍽️ Recipe App API

![Version](https://img.shields.io/badge/version-v1-blue.svg?cacheSeconds=2592000)

A Django-based Recipe Management API built with best practices in mind — including **Docker**, **Docker Compose**, **GitHub Actions CI**, **JWT authentication**, and **Test-Driven Development** (TDD).  
Designed to be secure, scalable, and easy to use for managing recipes, tags, ingredients, and user authentication.

---

## 🚀 Features

- **User Authentication**
  - Register with email and password.
  - Login with JWT token-based authentication.
  - Secure user endpoints using custom permissions.

- **Recipe Management**
  - Create, retrieve, update, and delete recipes.
  - Upload and manage recipe images.
  - Filter recipes by tags and ingredients.
  - Assign multiple tags and ingredients to a recipe.

- **Tag & Ingredient Management**
  - Create, list, and filter tags and ingredients.
  - Filter by "assigned only" to show only those linked to recipes.

- **Testing & Quality**
  - 100% test coverage using **TDD** with `unittest`.
  - CI pipeline via **GitHub Actions**, using Docker secrets for security.

---

## 🐳 Docker & CI/CD

This project is fully containerized:

- **Docker**: Runs the Django app in an isolated environment.
- **Docker Compose**: Orchestrates app, Postgres DB, and optional services.
- **GitHub Actions**:
  - Builds and runs tests in a Docker container.
  - Uses **Docker secrets** to handle sensitive data like env variables securely.
  - Lints and runs test suite on every push and pull request.

---

## 🔧 Run Locally with Docker

Clone the project:

```bash
git clone https://github.com/your-username/recipe-app-api.git
cd recipe-app-api
```
## Build and run with Docker Compose:
```bash
    docker compose build

    docker compose up
```

## To run the tests in the container:
```bash
    docker compose run --rm app sh -c "python manage.py test"
```

## To create a superuser:
```bash
    docker compose run --rm app sh -c "python manage.py createsuperuser"
```

# 📘 API Reference — Recipe App API

This document outlines all the available endpoints in the Recipe App API, grouped by functional areas.

---

## 🔐 User Endpoints (Authentication)

| Method | Endpoint                | Description                   |
|--------|-------------------------|-------------------------------|
| POST   | `/api/user/create/`     | Register a new user           |
| POST   | `/api/user/token/`      | Obtain JWT access and refresh tokens |
| POST   | `/api/user/token/refresh/` | Refresh JWT token            |
| GET    | `/api/user/me/`         | Get current authenticated user |
| PATCH  | `/api/user/me/`         | Update authenticated user's details |

---

## 🍽️ Recipe Endpoints

| Method | Endpoint                            | Description                       |
|--------|-------------------------------------|-----------------------------------|
| GET    | `/api/recipe/recipes/`              | List all recipes                  |
| POST   | `/api/recipe/recipes/`              | Create a new recipe               |
| GET    | `/api/recipe/recipes/:id/`          | Retrieve details of a recipe      |
| PUT    | `/api/recipe/recipes/:id/`          | Fully update a recipe             |
| PATCH  | `/api/recipe/recipes/:id/`          | Partially update a recipe         |
| DELETE | `/api/recipe/recipes/:id/`          | Delete a recipe                   |
| POST   | `/api/recipe/recipes/:id/upload-image/` | Upload image for a recipe     |

**Query Parameters (on GET `/recipes/`):**
- `tags`: Filter by tag IDs (comma-separated).
- `ingredients`: Filter by ingredient IDs (comma-separated).

---

## 🏷️ Tag Endpoints

| Method | Endpoint                | Description                      |
|--------|-------------------------|----------------------------------|
| GET    | `/api/recipe/tags/`     | List all tags                    |
| POST   | `/api/recipe/tags/`     | Create a new tag                 |
| GET    | `/api/recipe/tags/:id/` | Retrieve a specific tag          |
| PATCH  | `/api/recipe/tags/:id/` | Partially update a tag           |
| DELETE | `/api/recipe/tags/:id/` | Delete a tag                     |

**Query Parameters (on GET `/tags/`):**
- `assigned_only=1`: Return only tags assigned to at least one recipe.

---

## 🧂 Ingredient Endpoints

| Method | Endpoint                     | Description                       |
|--------|------------------------------|-----------------------------------|
| GET    | `/api/recipe/ingredients/`   | List all ingredients              |
| POST   | `/api/recipe/ingredients/`   | Create a new ingredient           |
| GET    | `/api/recipe/ingredients/:id/` | Retrieve a specific ingredient  |
| PATCH  | `/api/recipe/ingredients/:id/` | Partially update an ingredient  |
| DELETE | `/api/recipe/ingredients/:id/` | Delete an ingredient            |

**Query Parameters (on GET `/ingredients/`):**
- `assigned_only=1`: Return only ingredients assigned to at least one recipe.

---

## 🖼️ Recipe Image Upload

| Method | Endpoint                              | Description               |
|--------|---------------------------------------|---------------------------|
| POST   | `/api/recipe/recipes/:id/upload-image/` | Upload image for recipe |

**Payload:**
- Multipart form with image file under key `image`.

---

## 🔐 Authorization

All recipe, tag, and ingredient endpoints require **Token Authentication**.


## Author

👤 **Symon**

- Github: [@sin1ter](https://github.com/its-symon)
