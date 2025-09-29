# Application Architecture

This document describes the high-level architecture of the "Cards" application.

## 1. Overview

The application follows a decoupled **client-server** model, orchestrated via Docker containers. The backend is a **RESTful API** built with Laravel, and the frontend is a **Single Page Application (SPA)** built with Vue.js.

![Simple Architecture Diagram](https://i.imgur.com/O1z6p0a.png)

## 2. Core Components

### Backend (Laravel)

- **Framework:** Laravel (PHP).
- **Responsibility:** Exposes a REST API for the frontend to consume data. It handles all business logic, database interaction, and security.
- **Database:** Communicates with the MariaDB database through the **Eloquent** ORM.
- **Authentication:** (Future) Will manage user authentication and sessions via tokens or Laravel Sanctum.

### Frontend (Vue.js)

- **Framework:** Vue.js.
- **Responsibility:** Renders the entire user interface. As an SPA, it loads once and then fetches all data dynamically through API calls to the backend.
- **State Management:** Manages the application's state locally (e.g., the current card, selected category).
- **Components:** The UI is divided into reusable components (e.g., `Flashcard.vue`, `CategoryList.vue`).

### Database (MariaDB)

- **Engine:** MariaDB.
- **Role:** Stores all persistent application data, such as users, categories, cards, etc.
- **Access:** Only the Laravel backend has direct access to the database.

### Orchestration (Docker Compose)

- **Tool:** Docker Compose.
- **Role:** Defines and manages all the necessary services for the local development environment in isolated containers. This ensures a consistent environment across different developers.
- **Defined Services:**
  - `laravel`: The main application container with PHP and the web server.
  - `mariadb`: The database service.
  - `phpmyadmin`: A web interface to easily manage the database.

## 3. Data Flow

### Initial Setup Flow (Seeding)

1.  A developer places the `flashcards.json` file in `src/database/data/`.
2.  The `php artisan migrate --seed` command is executed.
3.  Laravel reads the JSON file, and a **Seeder** inserts the data into the corresponding tables in the **MariaDB** database.

### Runtime Data Flow

1.  The user opens the application in their browser.
2.  The browser loads the **Vue.js SPA**.
3.  A main Vue.js component makes an HTTP request (e.g., `GET /api/cards`) to the **Laravel API**.
4.  The Laravel controller receives the request and queries the data from **MariaDB** using an Eloquent model.
5.  Laravel serializes the results into JSON format and returns them in the HTTP response.
6.  The **Vue.js** application receives the data and uses it to dynamically render the categories and cards in the interface.
