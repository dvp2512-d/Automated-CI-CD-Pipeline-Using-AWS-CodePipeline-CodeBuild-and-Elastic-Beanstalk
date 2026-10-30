# Automated CI/CD Pipeline Using AWS CodePipeline, CodeBuild, and Elastic Beanstalk

A modern, production-style DevOps project that automates the build, test, quality analysis, and deployment of a multi-tier Java web application on AWS. This repository demonstrates how to deploy a Spring-based application using AWS CodePipeline, AWS CodeBuild, and Elastic Beanstalk, with supporting infrastructure automation for a complete CI/CD workflow.

## Overview

This project packages a Java web application named VProfile with a full CI/CD flow:

- Source code is built with Maven
- Unit and integration tests are executed
- Code quality checks are performed with Checkstyle and SonarQube
- The WAR artifact is stored or published to a repository manager
- The application is deployed through AWS infrastructure using CodePipeline + CodeBuild + Elastic Beanstalk

It is designed as a learning and demonstration project for cloud deployment automation, continuous delivery, and application modernization.

## Architecture

```text
Developer / Git Repository
          |
          v
AWS CodePipeline
          |
          v
AWS CodeBuild
  - Maven build
  - Test execution
  - Packaging WAR
  - Quality checks
          |
          v
Elastic Beanstalk
  - Web app deployment
  - Auto scaling / runtime management
          |
          v
Application Services
  - MySQL
  - Memcached
  - RabbitMQ
  - Elasticsearch
```

## Tech Stack

- Java 17
- Spring MVC
- Spring Security
- Spring Data JPA
- Hibernate
- Maven
- MySQL
- Memcached
- RabbitMQ
- Elasticsearch
- Jenkins (pipeline included)
- AWS CodePipeline
- AWS CodeBuild
- AWS Elastic Beanstalk
- SonarQube
- Nexus Repository Manager

## Features

- Multi-tier Spring web application architecture
- CI/CD pipeline automation for build and deployment
- Web application deployment on AWS Elastic Beanstalk
- Automated testing and static analysis
- Database-backed application configuration
- Infrastructure configuration templates for AWS and automation tools
- Jenkins pipeline for local CI experimentation

## Repository Structure

```text
.
├── .gitignore
├── Jenkinsfile
├── pom.xml
├── settings.xml
├── README.md
├── ansible/
├── aws-files/
│   ├── buildspec.yml
│   ├── build_buildspec.yml
│   ├── sonar_buildspec.yml
│   └── ssh_config_file
├── META-INF/
├── src/
│   ├── main/
│   │   ├── java/
│   │   ├── resources/
│   │   └── webapp/
│   └── test/
├── vagrant/
└── ...
```

## Prerequisites

Before running the application locally, ensure you have the following installed:

- JDK 17+
- Maven 3.9+
- MySQL 8+
- Git
- Optional: Jenkins, SonarQube, Nexus, AWS CLI

## Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/dvp2512-d/Automated-CI-CD-Pipeline-Using-AWS-CodePipeline-CodeBuild-and-Elastic-Beanstalk.git
cd Automated-CI-CD-Pipeline-Using-AWS-CodePipeline-CodeBuild-and-Elastic-Beanstalk
```

### 2. Configure the database

This project expects a MySQL database. Import the SQL backup file provided in the project:

```bash
mysql -u <username> -p <database_name> < src/main/resources/db_backup.sql
```

The application uses database details configured in:

- `src/main/resources/application.properties`

### 3. Build the project

```bash
mvn clean install -DskipTests
```

### 4. Run the application

This project includes a Jetty Maven plugin, so you can run it locally with:

```bash
mvn jetty:run
```

Once the application starts, browse to:

```text
http://localhost:8080
```

## Database Configuration

The app is configured for MySQL and uses database connectivity parameters from `src/main/resources/application.properties`.

Example configuration:

```properties
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://db01:3306/accounts?useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull
jdbc.username=admin
jdbc.password=admin123
```

> Update the database host, username, and password to match your local or AWS environment.

## CI/CD Pipeline

### Jenkins pipeline

The project includes a `Jenkinsfile` with pipeline stages for:

- Build
- Unit test
- Integration test
- Checkstyle analysis
- SonarQube quality gate
- Nexus artifact publishing

This file shows how the application can be built and validated continuously in a CI environment.

### AWS pipeline assets

The `aws-files/` directory contains AWS-specific build definitions for:

- `buildspec.yml` — standard AWS CodeBuild build configuration
- `build_buildspec.yml` — additional build definition
- `sonar_buildspec.yml` — SonarQube integration for CodeBuild
- `ssh_config_file` — SSH configuration support

These files are used to wire the repository into an AWS CodePipeline environment for automated deployment to Elastic Beanstalk.

## Build and Test Commands

```bash
# Clean build
mvn clean install

# Run unit tests
mvn test

# Run integration verification
mvn verify -DskipUnitTests

# Run Checkstyle
mvn checkstyle:checkstyle

# Run locally with Jetty
mvn jetty:run
```

## Deployment Notes

This repository is structured for deployment in AWS using a typical CodePipeline lifecycle:

1. Source stage pulls the repository
2. Build stage runs Maven and package generation
3. Test/quality stage validates the application
4. Deploy stage pushes the built artifact to Elastic Beanstalk

This enables continuous delivery with repeatable, automated deployments.

## Security and Quality Checks

The pipeline includes support for:

- SonarQube static analysis
- Checkstyle validation
- Reusable artifact packaging
- Secure integration with repository managers and deployment systems

## Project Goals

This project demonstrates:

- End-to-end CI/CD implementation
- Cloud-native AWS deployment patterns
- Java web application packaging and deployment
- DevOps automation and build verification
- Infrastructure-as-code and pipeline-driven delivery

## License

This project is intended for educational and demonstration purposes. Please review any included third-party dependencies and AWS configuration files before using them in production.

## Acknowledgements

This project is based on a multi-tier Java application architecture and is designed to showcase modern DevOps best practices for automated software delivery on AWS.

---

Built for cloud deployment automation, pipeline orchestration, and continuous delivery learning.
