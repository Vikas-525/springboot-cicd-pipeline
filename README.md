# Spring Boot CI/CD Pipeline Automation

## Project Overview

This project demonstrates the automation of building, testing, containerizing, and deploying a Spring Boot Java application using a CI/CD pipeline.

Jenkins automates the workflow, Maven handles application testing and building, Docker creates the container image, Docker Hub stores the image, and Kubernetes (MicroK8s) deploys the application.

The application is deployed in an AWS EC2 environment and accessed through a web browser using a Kubernetes NodePort service.

## Objectives

- Automate application building and deployment.
- Integrate GitHub with Jenkins.
- Perform application testing and building using Maven.
- Containerize the application using Docker.
- Store and distribute Docker images through Docker Hub.
- Deploy the containerized application using Kubernetes.
- Access the deployed application through a web browser.

## Technologies Used

| Technology | Purpose |
|---|---|
| Java | Application programming language |
| Spring Boot | Application framework |
| GitHub | Source code management |
| Jenkins | CI/CD pipeline automation |
| AWS EC2 | Hosts the project environment |
| Linux | Operating system |
| Maven | Application testing and building |
| Docker | Application containerization |
| Docker Hub | Docker image registry |
| Kubernetes (MicroK8s) | Container deployment and management |
| YAML | Kubernetes configuration files |

## Project Architecture Diagram

The following diagram illustrates the flow of the application through the CI/CD pipeline, from source code management to deployment and browser access.

![Project Architecture Diagram](project-architecture.jpeg)

### Architecture Flow

**GitHub → Jenkins on AWS EC2 → Maven → Docker → Docker Hub → Kubernetes (MicroK8s) → Browser**

1. Source code is maintained in GitHub.
2. Jenkins retrieves the source code and orchestrates the pipeline.
3. Maven tests and builds the application.
4. Docker creates a container image.
5. Docker Hub stores the image.
6. Kubernetes deploys the application using the container image.
7. Users access the deployed application through a browser using the NodePort service.

## Jenkins CI/CD Pipeline

The following screenshot shows the Jenkins pipeline used to automate the application build, testing, Docker image publishing, and Kubernetes deployment.

![Jenkins CI/CD Pipeline](jenkins-pipeline.jpeg)

### Pipeline Stages

| Stage | Description |
|---|---|
| Code Checkout | Retrieves the source code from GitHub |
| Maven Unit Test | Executes unit tests |
| Maven Build | Builds and packages the application |
| Maven Integration Test | Runs the verification lifecycle |
| Build Docker Image | Creates the application Docker image |
| Push Image to Docker Hub | Publishes the image to Docker Hub |
| Deploy to Kubernetes | Applies Kubernetes deployment and service configurations |

## CI/CD Workflow

### 1. Source Code Management – GitHub

The Spring Boot application source code is maintained in a GitHub repository.

Jenkins checks out the source code as part of the pipeline. Automatic execution following a code push depends on the Jenkins job and repository trigger configuration.

### 2. Continuous Integration – Jenkins

Jenkins runs on an AWS EC2 instance and automates the pipeline stages.

It coordinates application testing, building, Docker image creation, image publishing, and Kubernetes deployment.

### 3. Application Testing and Build – Maven

Maven manages the application's build lifecycle.

The pipeline uses the following commands:

**Run unit tests**
```bash
mvn test
```

**Clean and build the application**
```bash
mvn clean install
```

**Run verification**
```bash
mvn verify
```

These commands execute their respective Maven lifecycle phases, including applicable tests and verification tasks.

### 4. Containerization – Docker

Docker packages the application into a container image using the project's Dockerfile.

Example:

```bash
docker build -t ci-pipeline .
```

The resulting image can be used to run the application in a containerized environment.

### 5. Image Registry – Docker Hub

The pipeline authenticates with Docker Hub, tags the Docker image, and pushes it to the remote registry.

Example:

```bash
docker tag ci-pipeline <dockerhub-username>/ci-pipeline:latest
docker push <dockerhub-username>/ci-pipeline:latest
```

The image can then be pulled by the Kubernetes environment.

### 6. Deployment – Kubernetes (MicroK8s)

Kubernetes is used to deploy and manage the containerized application.

The project uses two YAML configuration files:

- **`deployment.yaml`** – Defines the application deployment and container configuration.
- **`service.yaml`** – Defines the NodePort service used to expose the application.

Jenkins applies the configurations using:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### 7. Application Access

After successful deployment, the application can be accessed through a web browser using the EC2 public IP address and configured NodePort.

```text
http://<EC2-Public-IP>:<NodePort>
```

The EC2 security group and Kubernetes service must permit the required network traffic.

## Application Output

The deployed application displays the following message:

```text
Welcome to our DevOps Project !!
```

## Project Structure

```text
springboot-cicd-pipeline/
│
├── images/
│   ├── project-architecture.jpeg
│   └── jenkins-pipeline.jpeg
│
├── src/
│   ├── main/
│   │   ├── java/com/javatechie/
│   │   │   └── DevopsIntegrationApplication.java
│   │   └── resources/
│   │
│   └── test/
│       └── java/com/javatechie/
│           └── DevopsIntegrationApplicationTests.java
│
├── .gitignore
├── Dockerfile
├── deployment.yaml
├── service.yaml
├── Jenkinsfile
├── mvnw
├── mvnw.cmd
├── pom.xml
└── README.md
```

*Note: This represents the intended project structure. Keep the filenames and directories consistent with the files actually present in your repository.*

## Key Learnings

Through this project, I gained practical experience in:

- Managing source code using GitHub.
- Automating CI/CD workflows with Jenkins.
- Building and testing Java applications using Maven.
- Creating and publishing Docker images.
- Working with Docker Hub as a container registry.
- Deploying containerized applications using Kubernetes.
- Using AWS EC2 and Linux environments.
- Understanding the end-to-end CI/CD process.

## Future Improvements

- Configure and verify automated pipeline triggers using GitHub webhooks.
- Add pipeline failure notifications.
- Introduce application monitoring and centralized logging.
- Implement automated security scanning.
- Explore safer Kubernetes deployment strategies.

