BlogSpot Blogging Platform - Backend
====================================

This repository contains the **Node.js (Express)** backend API for the BlogSpot Blogging Platform. It's responsible for handling all server-side logic, including user authentication, blog post data management, and interactions with the **MySQL** database.

💡 Problem Statement & Approach
-------------------------------

The core problem addressed is building a full-stack blogging platform where users can sign up, log in, and manage their own blog posts (create, edit, delete). My approach for the backend focuses on creating a secure, efficient, and well-structured API:

-   **RESTful API Design:** Implementing clear and consistent API endpoints (e.g., `/api/auth`, `/api/posts`, `/api/users/me/posts`) following REST principles for easy consumption by the frontend.

-   **Secure Authentication:** Utilizing **JSON Web Tokens (JWT)** for stateless authentication, combined with **Bcrypt** for robust password hashing and security.

-   **Robust Database Integration:** Employing `mysql2` for efficient and secure communication with the MySQL database, ensuring reliable data storage and retrieval for users and posts.

-   **Environment Variable Management:** Using `dotenv` to securely manage sensitive information like database credentials and JWT secrets, keeping them isolated from the codebase and facilitating easy configuration.

-   **Modular Structure:** Organizing the backend into logical modules (e.g., `routes`, `controllers`, `db.js` for database connection) to enhance maintainability, scalability, and code readability.

✨ Features
----------

-   **User Authentication API**: Provides endpoints for secure user signup (`/auth/register`), login (`/auth/login`), and session logout.

-   **Post Management API**: Offers comprehensive CRUD (Create, Read, Update, Delete) operations for blog posts.

-   **User-Specific Post Retrieval**: An authenticated endpoint (`/users/me/posts`) to fetch all posts created by the currently logged-in user.

-   **Secure Data Handling**: Implements password hashing with Bcrypt and utilizes JWTs for secure user sessions.

-   **Database Integration**: Connects to a MySQL database to persist all user accounts and blog post content.

🚀 Technologies Used
--------------------

-   **Node.js**: JavaScript runtime environment for building the server-side application.

-   **Express.js**: A fast, unopinionated, minimalist web framework for Node.js, used for building the RESTful API.

-   **MySQL2**: A powerful and efficient Node.js MySQL client for interacting with the database.

-   **JSON Web Tokens (JWT)**: Used for stateless user authentication and authorization.

-   **Bcrypt**: A library for hashing and salting passwords securely.

-   **Dotenv**: Manages environment variables, loading them from a `.env` file.

-   **Cookie-Parser**: Middleware to parse HTTP cookies attached to the client request.

-   **CORS**: Middleware to enable Cross-Origin Resource Sharing.

🛠️ Setup and Installation
--------------------------

Follow these steps to get the backend server running on your local machine.

1.  **Clone the Repository:** If you haven't already, clone the main project repository (which contains both frontend and backend folders):

    ```
    git clone https://github.com/nishant-deshmukh/BlogSpot-Blogging-Platform.git
    cd BlogSpot-Blogging-Platform

    ```

    *Note: This README assumes you've cloned the main project containing both `Client` and `Server` directories.*

2.  **Navigate to the Backend Directory:**

    ```
    cd Server

    ```

3.  **Install Dependencies:** Install all necessary Node.js packages as listed in `package.json`:

    ```
    npm install

    ```

4.  **Database Configuration (`.env` file):** Create a `.env` file in the `Server` directory. This file will hold your database credentials and other sensitive information. **It is crucial that you do NOT commit this file to Git for security reasons.**

    ```
    # Server/.env
    DB_HOST=localhost
    DB_USER=your_mysql_username
    DB_PASSWORD=your_mysql_password
    DB_DATABASE=your_database_name
    JWT_SECRET=a_very_secret_key_for_jwt_signing # IMPORTANT: Replace with a strong, random string

    ```

    **Remember to replace `your_mysql_username`, `your_mysql_password`, `your_database_name`, and `a_very_secret_key_for_jwt_signing` with your actual MySQL database credentials and a secure JWT secret.**

5.  **Database Schema Setup:** You'll need to set up your MySQL database and tables. Here's a basic SQL schema to get started:

    ```
    -- Create Database
    CREATE DATABASE IF NOT EXISTS blogapp_db;
    USE blogapp_db;

    -- Create Users Table
    CREATE TABLE IF NOT EXISTS users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        username VARCHAR(255) NOT NULL UNIQUE,
        email VARCHAR(255) NOT NULL UNIQUE,
        password VARCHAR(255) NOT NULL,
        img VARCHAR(255), -- Optional: for user profile image
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );

    -- Create Posts Table
    CREATE TABLE IF NOT EXISTS posts (
        id INT AUTO_INCREMENT PRIMARY KEY,
        title VARCHAR(255) NOT NULL,
        content TEXT NOT NULL,
        img VARCHAR(255), -- Optional: for post header image
        date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        uid INT NOT NULL,
        FOREIGN KEY (uid) REFERENCES users(id) ON DELETE CASCADE
    );

    ```

    **Note:** Ensure your database name matches the `DB_DATABASE` variable in your `.env` file.

🏃 Running the Backend Server
-----------------------------

1.  **Start the Node.js Server:** From within the `Server` directory:

    ```
    node index.js

    ```

    The backend server should start and be accessible at `http://localhost:8080`.

🧪 API Endpoints (Postman/cURL)
-------------------------------

You can test the API endpoints using Postman, Insomnia, or cURL. The base URL for all API calls is `http://localhost:8080/api`.

| **Method** | **Endpoint** | **Description** | **Authentication Required** |
| --- | --- | --- | --- |
| POST | /auth/login | Authenticate user and receive JWT token. | No |
| POST | /auth/register | Register a new user. | No |
| POST | /posts | Create a new blog post. | Yes (JWT in Header) |
| GET | /posts | Retrieve all public blog posts. | No |
| GET | /posts/:id | Retrieve a single blog post by ID. | No |
| PUT | /posts/:id | Update an existing blog post by ID. | Yes (JWT in Header) |
| DELETE | /posts/:id | Delete a blog post by ID. | Yes (JWT in Header) |
| GET | /users/me/posts | Retrieve all blog posts by the authenticated user. | Yes (JWT in Header) |

**Example Request Header for Authenticated Endpoints:**

```
Authorization: Bearer <your_jwt_token_here>

```

🤖 AI Usage in Development
--------------------------

This project leveraged AI tools (such as Cursor AI/Codium, ChatGPT, or Claude) to assist in various development stages, including:

-   Generating boilerplate code for API routes, controllers, and database interaction functions.

-   Debugging and troubleshooting server-side logic and database connectivity issues.

-   Refactoring code for improved security (e.g., password hashing, JWT handling) and performance.

-   Suggesting best practices for backend architecture and RESTful API design.

-   Drafting comprehensive documentation and README content.

This collaborative approach with AI tools significantly enhanced development efficiency and allowed for a focused effort on delivering high-quality, robust, and secure backend solutions. "Make it stand out. Make it yours."

🚧 Challenges Faced
-------------------

Developing this full-stack blogging platform within a tight deadline of just **3 days** presented a significant challenge. Key difficulties encountered along the way included:

-   **Time Management:** Balancing the development of both frontend and backend components, database setup, and API integration within the limited timeframe.

-   **Authentication & Authorization:** Implementing secure user authentication with JWTs and ensuring proper authorization for post management (e.g., only authors can edit/delete their posts).

-   **Database Schema & Queries:** Designing an efficient MySQL database schema and writing optimized SQL queries for various CRUD operations and user-specific data retrieval.

-   **API Design & Error Handling:** Crafting a clear and consistent RESTful API, including robust error handling for various scenarios (e.g., user not found, invalid token, unauthorized access).

-   **Cross-Origin Resource Sharing (CORS):** Properly configuring CORS to allow communication between the frontend and backend running on different ports.

-   **Debugging Across Stacks:** Identifying and resolving issues that spanned across the frontend, backend, and database layers, requiring a holistic understanding of the entire system.

Overcoming these challenges required focused effort, efficient problem-solving, and strategic use of available resources.

🎥 Demo
-------

A screen recording demonstrating all features of the BlogSpot Blogging Platform will be attached here.

[[Google Drive Public Link to Demo Video]](https://drive.google.com/file/d/1BA-lZw63A3D8Rr-EUn1Cfl_TsflVZiEI/view?usp=drive_link)
