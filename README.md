Here's the updated `README.md` with the "Database Design" section:

# Airbnb Clone Backend

---

## Overview

Welcome to the **Airbnb Clone Backend** project! This project aims to build a robust and scalable backend system that mimics the core functionalities of Airbnb. Our goal is to provide a solid foundation for managing user interactions, property listings, bookings, and payments, ensuring a seamless experience for both users and hosts. This project serves as a comprehensive, real-world application to deepen your understanding of full-stack development, backend architecture, database design, API development, and application security.

---

## Project Goals

Our primary goals for this project include:

* **User Management:** Implementing a secure system for user registration, authentication, and profile management.
* **Property Management:** Developing features for property listing creation, updates, and retrieval.
* **Booking System:** Creating a booking mechanism for users to reserve properties and manage booking details.
* **Payment Processing:** Integrating a payment system to handle transactions and record payment details.
* **Review System:** Allowing users to leave reviews and ratings for properties.
* **Data Optimization:** Ensuring efficient data retrieval and storage through database optimizations.

---

## Technology Stack

The backend for the Airbnb Clone is built using a modern and powerful technology stack to ensure scalability, performance, and maintainability:

* **Django:** A high-level Python web framework used for building the RESTful API and handling core business logic.
* **Django REST Framework:** Provides a comprehensive toolkit for creating and managing RESTful APIs with ease.
* **PostgreSQL:** A powerful, open-source relational database used for robust and scalable data storage.
* **GraphQL:** Offers a flexible and efficient query language for interacting with the backend, allowing clients to request exactly the data they need.
* **Celery:** An asynchronous task queue used for handling long-running or resource-intensive tasks, such as sending notifications or processing payments, without blocking the main application thread.
* **Redis:** An in-memory data structure store used for caching frequently accessed data to reduce database load and improve response times, as well as for session management.
* **Docker:** A containerization platform used to create consistent and isolated development and deployment environments, ensuring the application runs the same way everywhere.
* **CI/CD Pipelines (e.g., GitHub Actions):** Automated pipelines for continuous integration and continuous deployment, enabling automated testing, building, and deployment of code changes, leading to faster and more reliable releases.

---

## Team Roles

A successful software development project relies on a collaborative and well-defined team structure. For the Airbnb Clone backend, the following key roles are essential, each with specific responsibilities:

* **Backend Developer:**
    * **Description:** Engineers and stabilizes the product, focusing on the core logic and functionality that operates behind the scenes.
    * **Responsibility in Project:** Responsible for implementing API endpoints, designing and implementing database schemas, writing business logic, and ensuring the stability and performance of the backend services. They will work with Django and Django REST Framework to build out the core features.

* **Database Administrator (DBA):**
    * **Description:** Manages the database systems, ensuring data integrity, availability, and performance.
    * **Responsibility in Project:** Manages database design, including defining entities, attributes, and relationships. They are responsible for implementing indexing for fast data retrieval, setting up caching strategies with Redis to optimize database load, and ensuring overall database health and security in PostgreSQL.

* **DevOps Engineer:**
    * **Description:** Facilitates cooperation between development and operations teams, building continuous integration and continuous delivery (CI/CD) pipelines for faster and more reliable delivery.
    * **Responsibility in Project:** Handles deployment, monitoring, and scaling of the backend services. They will set up and maintain Docker containers for consistent environments and implement CI/CD pipelines (e.g., using GitHub Actions) for automated testing and deployment of code changes.

* **QA Engineer:**
    * **Description:** Makes sure an application performs according to requirements and spots functional and non-functional defects.
    * **Responsibility in Project:** Ensures the backend functionalities are thoroughly tested and meet quality standards. They will design and execute test cases for API endpoints, identify and report bugs, and work closely with developers to ensure a high-quality product.

---

## Database Design

The database design is critical for the efficient storage and retrieval of all project data. We will use **PostgreSQL** as our relational database management system. Below are the key entities and their relationships:

### Key Entities

* **Users**
    * `user_id` (Primary Key)
    * `username` (Unique)
    * `email` (Unique)
    * `password_hash`
    * `registration_date`

* **Properties**
    * `property_id` (Primary Key)
    * `host_id` (Foreign Key to Users)
    * `title`
    * `description`
    * `price_per_night`
    * `location`
    * `availability_status`

* **Bookings**
    * `booking_id` (Primary Key)
    * `user_id` (Foreign Key to Users)
    * `property_id` (Foreign Key to Properties)
    * `check_in_date`
    * `check_out_date`
    * `total_price`
    * `booking_status` (e.g., pending, confirmed, cancelled)

* **Reviews**
    * `review_id` (Primary Key)
    * `user_id` (Foreign Key to Users)
    * `property_id` (Foreign Key to Properties)
    * `rating` (1-5 stars)
    * `comment`
    * `review_date`

* **Payments**
    * `payment_id` (Primary Key)
    * `booking_id` (Foreign Key to Bookings)
    * `user_id` (Foreign Key to Users)
    * `amount`
    * `payment_date`
    * `payment_status` (e.g., successful, failed, pending)
    * `transaction_id` (from payment gateway)

### Entity Relationships

* **Users and Properties:** A `User` can be a host and therefore can list **multiple** `Properties`. Each `Property` belongs to **one** `User` (host).
* **Users and Bookings:** A `User` can make **multiple** `Bookings`. Each `Booking` is made by **one** `User`.
* **Properties and Bookings:** A `Property` can have **multiple** `Bookings`. Each `Booking` is for **one** `Property`.
* **Users and Reviews:** A `User` can write **multiple** `Reviews`. Each `Review` is written by **one** `User`.
* **Properties and Reviews:** A `Property` can receive **multiple** `Reviews`. Each `Review` is for **one** `Property`.
* **Bookings and Payments:** Each `Booking` can have **one** `Payment` associated with it (or multiple if partial payments are allowed, but for simplicity, we'll assume one primary payment). Each `Payment` is tied to **one** `Booking`.
* **Users and Payments:** A `User` can initiate **multiple** `Payments` for various bookings. Each `Payment` is initiated by **one** `User`.
