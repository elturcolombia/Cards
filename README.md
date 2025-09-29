# Cards 🎴✨

A web application to study **English flashcards** using **Laravel + Vue.js + Docker**.

---

## 🎯 Project Summary

This application provides an interactive and organized way to study English phrases. The card information is managed in a database and consumed via a REST API.

The interface, built with Vue.js, presents the cards by category and allows for a fluid study experience with "flippable" cards that include the phrase, its pronunciation, the Spanish translation, and a glossary of key terms.

---

## 🚀 Tech Stack

- **Backend:** [Laravel](https://laravel.com/)
- **Frontend:** [Vue.js](https://vuejs.org/)
- **Database:** [MariaDB](https://mariadb.org/)
- **Orchestration:** [Docker Compose](https://docs.docker.com/compose/)
- **Web Server:** Nginx (implied in the Laravel/Sail image)
- **DB Management:** [phpMyAdmin](https://www.phpmyadmin.net/)

---

## 🏁 Local Environment Setup

Follow these steps to deploy a complete local development environment.

### Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop/) and [Docker Compose](https://docs.docker.com/compose/install/) must be installed on your system.
- [Git](https://git-scm.com/) to clone the repository.

### Installation Steps

1.  **Clone the repository:**
    ```bash
    git clone <repository-URL>
    cd Cards
    ```

2.  **Configure the Laravel environment:**
    Copy the example environment file. The default configuration is already compatible with Docker.
    ```bash
    cp src/.env.example src/.env
    ```

3.  **Prepare Data for Seeding:**
    The initial setup script (seeder) will look for a JSON file to populate the database. Place your flashcards file at the following path:
    ```bash
    mkdir -p src/database/data
    cp english_flashcards_final.json src/database/data/flashcards.json
    ```

4.  **Build and run the Docker containers:**
    This command will build and run all services (Laravel, MariaDB, etc.) in the background.
    ```bash
    docker-compose up -d --build
    ```

5.  **Install dependencies:**
    Once the containers are running, execute the Composer (PHP) and NPM (JS) dependency installers.
    ```bash
    docker-compose exec laravel composer install
    docker-compose exec laravel npm install
    ```

6.  **Set up and Seed the Application:**
    The following commands will prepare the application and database. They will generate the app key, create the tables, and populate them with data from the JSON file.
    ```bash
    # Generate the application key
    docker-compose exec laravel php artisan key:generate

    # Run migrations (create tables) and seeders (populate tables)
    docker-compose exec laravel php artisan migrate --seed
    ```

That's it! Your local development environment is now configured, the database is seeded, and the application is running.

---

## 💻 Development

-   **Accessing the application:**
    The application will be available in your browser at [http://localhost:8000](http://localhost:8000).

-   **Starting and stopping the environment:**
    ```bash
    # Start all services in the background
    docker-compose up -d

    # Stop all services
    docker-compose down
    ```

-   **Compiling assets (Vue.js):**
    To compile Vue.js files and see frontend changes as you develop, run:
    ```bash
    docker-compose exec laravel npm run dev
    ```
    This will start Vite in "watch" mode, automatically reloading the browser on changes.

-   **Running Artisan commands:**
    To use the Laravel command line, execute it through `docker-compose exec`:
    ```bash
    docker-compose exec laravel php artisan <command>
    ```
    *Example: `docker-compose exec laravel php artisan make:controller TestController`*

-   **Database Access:**
    You can manage the MariaDB database via phpMyAdmin at [http://localhost:8080](http://localhost:8080).