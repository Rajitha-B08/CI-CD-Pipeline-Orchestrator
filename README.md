# CI/CD Pipeline Orchestrator

A mini CI/CD Pipeline Orchestrator built using Java, Spring Boot, and MySQL to simulate how modern software delivery pipelines work. This project was created to understand backend system design, multithreading, task scheduling, and workflow automation concepts commonly used in DevOps tools such as Jenkins and GitLab CI/CD.

The application allows users to create and execute pipelines consisting of Build, Test, and Deploy stages, while tracking execution status, handling failures, and storing logs for monitoring and debugging.

## Why I Built This Project

While learning backend development, I wanted to understand what happens behind the scenes when code is automatically built, tested, and deployed. Instead of using existing CI/CD tools, I decided to build a simplified orchestration system from scratch to explore concepts such as:

* REST API development
* Asynchronous task execution
* Multithreading in Java
* Job scheduling and queue management
* Database persistence
* Failure handling and retry mechanisms

## Features

### Pipeline Management

* Create and execute CI/CD pipelines
* Support for Build, Test, and Deploy stages
* Track pipeline execution status
* View execution history

### Concurrent Pipeline Execution

* Multiple pipelines can run simultaneously
* Uses ExecutorService and thread pools for efficient execution
* BlockingQueue is used to manage incoming jobs

### Retry and Failure Handling

* Automatically retries failed stages
* Prevents a single failure from affecting other running pipelines
* Tracks successful and failed executions

### Logging and Monitoring

* Stores execution status in MySQL
* Maintains logs for debugging and auditing
* Allows users to check pipeline progress at any time

### REST APIs

* Start a new pipeline
* Check pipeline status
* Retrieve execution details
* Monitor pipeline history

## Tech Stack

### Backend

* Java 17
* Spring Boot
* Spring Data JPA

### Database

* MySQL

### Concurrency

* ExecutorService
* BlockingQueue
* Java Multithreading

### Tools

* Maven
* Postman
* VS Code / IntelliJ IDEA
* MySQL Workbench

## How It Works

1. A user sends a request to start a pipeline.
2. The pipeline is stored in the database with a **PENDING** status.
3. The job is added to a queue.
4. Worker threads pick jobs from the queue and start execution.
5. Each stage (Build, Test, Deploy) is processed sequentially.
6. If a stage fails, the retry mechanism attempts to run it again.
7. Pipeline status and logs are continuously updated in the database.
8. Users can monitor progress through REST APIs.

## Project Structure

src/main/java/com/example/cicd
│
├── controller
├── service
├── scheduler
├── repository
├── entity
├── dto
├── config
├── util
└── model


### Main Components

**Controller Layer**

* Handles API requests and responses.

**Service Layer**

* Contains the business logic for pipeline execution.

**Scheduler Layer**

* Manages job queues and background execution.

**Repository Layer**

* Handles database operations.

**Execution Engine**

* Executes Build, Test, and Deploy stages.

## Sample API Endpoints

### Start Pipeline

```http
POST /pipeline/start
```

Request:

```json
{
  "stages": ["build", "test", "deploy"]
}
```

Response:

```json
{
  "jobId": 1,
  "status": "PENDING"
}
```

### Get Pipeline Status

```http
GET /pipeline/{id}
```

Response:

```json
{
  "jobId": 1,
  "status": "RUNNING"
}
```

## What I Learned

Building this project helped me gain hands-on experience with:

* Spring Boot application development
* REST API design
* Java multithreading
* ExecutorService and thread pools
* Queue-based job scheduling
* Database integration with JPA
* Error handling and retry strategies
* Designing scalable backend systems

## Future Improvements

Some features I would like to add in future versions:

* Web-based dashboard for monitoring pipelines
* Real-time execution updates
* Stage-level execution history
* User authentication and authorization
* Notifications for pipeline completion
* Docker integration
* GitHub Actions or Jenkins integration

## Conclusion

This project was a great opportunity to explore how CI/CD systems work internally while improving my backend development skills. It combines API development, concurrency, database management, and workflow orchestration into a single application and serves as a practical introduction to DevOps-inspired system design.
