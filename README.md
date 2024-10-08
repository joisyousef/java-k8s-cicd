---

# Java Kubernetes CI/CD Pipeline

This repository demonstrates a complete CI/CD pipeline for a Java application using Jenkins, Docker, SonarQube, and Trivy. The application is built with Maven, analyzed for code quality, containerized with Docker, scanned for vulnerabilities, and deployed to a Kubernetes environment.

## Project Overview

This project demonstrates an automated CI/CD pipeline to build, test, analyze, and deploy a Java application using modern DevOps practices. The pipeline is designed to be run on Jenkins and uses Docker for containerization, SonarQube for code quality analysis, and Trivy for vulnerability scanning.

The primary features of this project include:

- **Automated Build and Test**: Using Maven to compile and package the application.
- **Static Code Analysis**: SonarQube is integrated into the pipeline to ensure code quality.
- **Containerization**: The application is built into a Docker image and pushed to Docker Hub.
- **Vulnerability Scanning**: Trivy is used to scan the Docker image for vulnerabilities.
- **Clean-Up**: Unused Docker artifacts are cleaned up after successful pipeline execution.

## Technologies Used

- **Jenkins**: Automation server for managing the CI/CD pipeline.
- **Maven**: Dependency management and build automation tool.
- **Docker**: For containerizing the Java application.
- **SonarQube**: For static code analysis and enforcing code quality gates.
- **Trivy**: For container image vulnerability scanning.
- **Git**: Version control system.

## Pipeline Stages

1. **Cleanup Workspace**: Clears the Jenkins workspace to avoid conflicts.
2. **Checkout from SCM**: Pulls the latest code from the GitHub repository.
3. **Build Application**: Builds the Java application using Maven.
4. **Test Application**: Runs unit tests using Maven.
5. **SonarQube Analysis**: Analyzes code quality and coverage using SonarQube.
6. **Quality Gate**: Verifies the results from SonarQube against the quality gate criteria.
7. **Build & Push Docker Image**: Builds a Docker image of the application and pushes it to Docker Hub.
8. **Trivy Scan**: Scans the Docker image for vulnerabilities.
9. **Cleanup Artifacts**: Removes Docker images created during the pipeline to free up space.

## Setup Instructions

### Prerequisites

- Jenkins installed with Docker and SonarQube plugins.
- Docker Hub account for storing container images.
- SonarQube setup for code analysis.
- Trivy installed on the Jenkins server for image scanning.

### Jenkins Setup

1. Install the necessary plugins for Jenkins:

   - Docker Pipeline Plugin
   - SonarQube Scanner Plugin
   - Git Plugin

2. Configure Jenkins with the following tools:

   - JDK 21
   - Maven 3

3. Set up environment variables in Jenkins:

   - `DOCKER_USER`: Docker Hub username.
   - `DOCKER_PASS`: Docker Hub credentials.
   - `GITHUB_TOKEN`: Token for accessing the GitHub repository.
   - `SONARQUBE_TOKEN`: Token for authenticating with SonarQube.

4. Create a Jenkins pipeline job and point it to this repository.

### Docker Setup

- Ensure Docker is installed and running on the Jenkins node where the build will happen.
- Set up Docker credentials in Jenkins for pushing images to Docker Hub.

### SonarQube Setup

- Configure SonarQube with your Jenkins instance for static code analysis.

### Trivy Setup

- Ensure Trivy is installed on the Jenkins server.
- The Trivy scan is integrated into the pipeline to scan the Docker images for vulnerabilities.
