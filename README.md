# Vending Machine Service
### A Spring Boot backend service simulating a vending machine

## Features
- **Secure REST APIs** with role-based access, JWT authentication, and token validation.
- **Global exception handling** with consistent error responses.
- **Aspect-Oriented Programming (AOP)** for access validation and cross-cutting concerns.
- **Comprehensive unit & integration test suite**.

## Infrastructure & Deployment
- **Fully containerized setup** using Docker for both the application and database.
- **Automatic database initialization** via `schema.sql` and `data.sql` to provision tables and seed default items on startup.
- **Docker Compose orchestration** for running the full environment with one command.
- **Environment-based configuration** using Spring Profiles for local, test, and containerized deployments.

## Tech Stack
- **Backend:** Java 17, Spring Boot (Web, Security, JPA)
- **Database:** MySQL (auto-initialized)
- **Build & Dependency Management:** Maven
- **Testing:** JUnit 5, Mockito, MockMvc
- **Containerization:** Docker, Docker Compose
---
 ## Requirements
- REST API should be implemented consuming and producing “application/json”.
- Implement a product model with amountAvailable, cost, productName and sellerId fields.
- Implement a user model with username, password, deposit and role fields.
- Implement CRUD for users (POST shouldn’t require authentication).
- Implement CRUD for a product model (GET can be called by anyone, while POST, PUT, and DELETE can be called only by the seller user who created the product).
- Implement /deposit endpoint so users with a “buyer” role can deposit 5, 10, 20, 50 and 100 cent coins into their vending machine account. 
- Implement /buy endpoint (accepts productId, amount of products) so users with a “buyer” role can buy products with the money they’ve deposited. API should return the total they’ve spent, products they’ve purchased and their change if there’s any (in 5, 10, 20, 50 and 100 cents coins).
- Implement /reset endpoint so users with a “buyer” role can reset their deposit.

## How to Run Vending Machine App with Docker

#### Prerequisites 
- Both `8080` and  `3306` ports are free as they will be consumed by the app.
- Docker and Docker Compose installed. (see [Notes](#notes) for versions recommendation)
- Create a `.env` file in the root directory of the project with the following variables ( contact me to get the values ):
  ```
  # Database Configuration
  MYSQL_DATABASE=vending_machine
  MYSQL_USER=your_DB_user
  MYSQL_PASSWORD=your_secure_password_here
  MYSQL_ROOT_PASSWORD=your_root_password_here
  
  # JWT Configuration
  JWT_SECRET_KEY=your_jwt_secret_key_here_make_it_long_and_secure
  ```


 #### Build & Run
I have added `Makefile` to make it easy for you to spin up the project.

#### All you need is to change the directory to the project root and run any of the following command based on your need: -

| Command    | Description                                                                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| make run   | This will build docker to install the necessary JVM version, use docker's maven version, build the project (without testcases) and start the services. |
| make stop  | This should stop and remove containers.                                                                                                                |                                                                                                 
| make reset | This will do `make stop` + will remove the cached DB volumes.                                                                                          |                             
## API Testing
- Download the [Postman Collection](vending-machine.postman_collection.json) to test the endpoints.
- Import this file in postman and check the APIs out.

## Notes
- The recommended versions of docker is `v24.x.x` and for docker-compose `v2.24.x+`
- The application will be available at `http://localhost:8080/api/v1` after running `make run`
- Default database will be created automatically with the schema from `src/main/resources/db/schema.sql`
- JWT tokens expire after 24 hours by default (configurable)

## Thanks
