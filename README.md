# Spring Boot CI/CD Pipeline Automation

## Project Overview
This project demonstrates a CI/CD pipeline for a Spring Boot Java application using Jenkins, Maven, Docker, Docker Hub, and Kubernetes.

The pipeline automates source code checkout, application testing, building, Docker image creation, publishing the image to Docker Hub, and deployment to Kubernetes.

## Technologies Used
- Java Spring Boot
- Git and GitHub
- Jenkins
- Apache Maven
- Docker
- Docker Hub
- Kubernetes (MicroK8s)
- AWS EC2
- Linux

## CI/CD Workflow
1. Source code checkout from GitHub.
2. Maven unit testing.
3. Maven build and verification.
4. Docker image creation.
5. Docker image push to Docker Hub.
6. Kubernetes deployment using deployment and service YAML files.
7. Application verification through a web browser.

## Kubernetes Configuration
- `deployment.yaml` — Defines the application deployment.
- `service.yaml` — Exposes the application through a Kubernetes NodePort service.

## Project Outcome
Successfully deployed the Spring Boot application and verified that it displayed:

**Welcome to our DevOps Project !!**

## Key Learnings
- CI/CD pipeline automation using Jenkins.
- Maven build and test stages.
- Docker image creation and publishing.
- Kubernetes application deployment.
- Troubleshooting container and deployment issues.

## Author
Vikas Jain P

## Acknowledgement
This project was developed using a starter project from the original repository. The implementation and configuration were used for learning CI/CD concepts.
