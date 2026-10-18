# Spring Boot CI/CD Pipeline Automation

## Project Overview
This project demonstrates the automation of a CI/CD pipeline for a Spring Boot Java application using Jenkins, Maven, Docker, Docker Hub, and Kubernetes.

The pipeline automates application checkout, testing, building, Docker image creation, and publishing the image to Docker Hub. The application is deployed to Kubernetes and made accessible through a NodePort service.

## Technologies Used
- AWS EC2
- Git and GitHub
- Jenkins
- Apache Maven
- Java Spring Boot
- Docker
- Docker Hub
- Kubernetes (MicroK8s)
- Linux

## CI/CD Workflow
1. Source code is maintained in GitHub.
2. Jenkins checks out the application code.
3. Maven runs tests and builds the application.
4. Docker builds a container image.
5. Jenkins pushes the image to Docker Hub.
6. Kubernetes runs the application in a container.
7. A NodePort service provides access to the deployed application.

## Deployment Verification
The deployed application was verified through a web browser and displayed:

**Welcome to our DevOps Project !!**

## Key Learnings
- Understanding CI/CD pipeline stages.
- Automating Maven builds and tests using Jenkins.
- Building and publishing Docker images.
- Deploying containerized applications to Kubernetes.
- Verifying application availability after deployment.

## Author
Vikas Jain P
