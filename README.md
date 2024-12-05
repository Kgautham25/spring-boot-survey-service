# Student Survey Microservice

_Last updated: December 05, 2024_

A Spring Boot REST microservice for collecting and managing student survey submissions, backed by MySQL, containerized with Docker, deployed to **Kubernetes**, and built through a **Jenkins** CI/CD pipeline.

> Course project for Software Engineering for the World Wide Web (SWE 645), George Mason University.

## Overview

The service exposes a CRUD REST API over student survey records. It was built to practice a full cloud deployment workflow: package the app as a container image, push it through Jenkins, and run it on a Kubernetes cluster (originally on AWS EC2/RDS).

## Features

- REST API to create, read, update, and delete survey entries.
- JPA/Hibernate persistence to a MySQL database.
- Containerized with a `Dockerfile`.
- Kubernetes deployment and service manifests (`deployment.yaml`, `service.yaml`).
- Jenkins pipeline (`Jenkinsfile`) for automated build and deploy.

## Tech stack

Java 17 · Spring Boot · Spring Data JPA · MySQL · Maven · Docker · Kubernetes · Jenkins

## Configuration

Database credentials are **not** hard-coded. The app reads them from environment variables:

| Variable | Meaning | Example |
| --- | --- | --- |
| `DB_URL` | JDBC URL | `jdbc:mysql://localhost:3306/appdb?useSSL=false&serverTimezone=UTC` |
| `DB_USERNAME` | DB user | `root` |
| `DB_PASSWORD` | DB password | *(set in your environment / k8s secret)* |

## Getting started

### Prerequisites
- Java 17+
- Maven
- A running MySQL instance

### Run locally
```bash
export DB_URL="jdbc:mysql://localhost:3306/appdb?useSSL=false&serverTimezone=UTC"
export DB_USERNAME="root"
export DB_PASSWORD="your-password"

./mvnw spring-boot:run
```
The API starts on `http://localhost:8081`.

### Build a container image
```bash
./mvnw clean package
docker build -t student-survey .
```

### Deploy to Kubernetes
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
> Provide `DB_PASSWORD` through a Kubernetes Secret rather than committing it.

## Author

Gautham Kumar Karamthot
