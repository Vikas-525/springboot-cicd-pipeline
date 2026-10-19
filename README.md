# Spring Boot CI/CD Pipeline Automation

## Project Overview

This project demonstrates the automation of building, testing, containerizing, and deploying a Spring Boot Java application using a CI/CD pipeline.

The pipeline integrates GitHub, Jenkins, Maven, Docker, Docker Hub, and Kubernetes (MicroK8s) to automate the application delivery process. AWS EC2 provides the environment for running the pipeline and deploying the application.

The deployed application is exposed through a Kubernetes NodePort service and can be accessed using a web browser.

## Objectives

- Automate application building and deployment using a CI/CD pipeline.
- Manage application source code using GitHub.
- Automate testing and building with Maven.
- Containerize the application using Docker.
- Store and distribute Docker images through Docker Hub.
- Deploy the application using Kubernetes.
- Understand the integration of cloud infrastructure and DevOps tools.

## Technologies Used

| Technology | Purpose |
|---|---|
| Java | Application programming language |
| Spring Boot | Application framework |
| GitHub | Source code management |
| Jenkins | CI/CD pipeline automation |
| AWS EC2 | Cloud-based compute environment |
| Linux | Operating system |
| Maven | Application testing and building |
| Docker | Application containerization |
| Docker Hub | Container image registry |
| Kubernetes (MicroK8s) | Container deployment and management |
| YAML | Kubernetes configuration files |

## Project Architecture

The architecture diagram illustrates how the different tools interact throughout the CI/CD workflow, from source code management to application deployment.

![Project Architecture](images/project-architecture.jpeg)

### Architecture Flow

**GitHub → Jenkins on AWS EC2 → Maven → Docker → Docker Hub → Kubernetes (MicroK8s) → NodePort Service → Web Browser**

1. Application source code is maintained in GitHub.
2. Jenkins checks out the source code and orchestrates the pipeline.
3. Maven performs application testing and building.
4. Docker creates a container image.
5. Docker Hub stores the container image.
6. Kubernetes deploys the application using the image.
7. A NodePort service exposes the application for browser access.

## Jenkins CI/CD Pipeline

The pipeline diagram below illustrates the stages involved in automating the application's build and deployment process.

![Jenkins CI/CD Pipeline](images/jenkins-pipeline.jpeg)

### Pipeline Stages

| Stage | Description |
|---|---|
| Code Checkout | Retrieves source code from GitHub |
| Maven Unit Test | Executes unit tests |
| Maven Build | Builds and packages the application |
| Maven Integration Test | Runs the Maven verification lifecycle |
| Build Docker Image | Creates the application container image |
| Push Image to Docker Hub | Publishes the image to Docker Hub |
| Deploy to Kubernetes | Applies Kubernetes deployment and service configurations |

## CI/CD Workflow

### 1. Source Code Management – GitHub

GitHub stores the Spring Boot application's source code. Jenkins retrieves the code as part of the pipeline.

Automatic pipeline execution after a code push depends on the Jenkins job and repository trigger configuration.

### 2. Continuous Integration – Jenkins

Jenkins runs on AWS EC2 and orchestrates the CI/CD workflow.

It automates source code checkout, application testing, building, Docker image creation, image publishing, and Kubernetes deployment.

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

Docker packages the Spring Boot application into a container image using the project's Dockerfile.

Example command:

```bash
docker build -t ci-pipeline .
```

The resulting image can be used to run the application in a containerized environment.

### 5. Image Registry – Docker Hub

After the Docker image is built, Jenkins authenticates with Docker Hub, tags the image, and pushes it to the registry.

Example commands:

```bash
docker tag ci-pipeline <dockerhub-username>/ci-pipeline:latest
docker push <dockerhub-username>/ci-pipeline:latest
```

The image is then available for the Kubernetes environment to pull and deploy.

### 6. Deployment – Kubernetes (MicroK8s)

Kubernetes is used to deploy and manage the containerized application.

The project uses the following configuration files:

- **`deployment.yaml`** – Defines the application deployment and container configuration.
- **`service.yaml`** – Defines the NodePort service used to expose the application.

Jenkins applies the Kubernetes configurations using:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### 7. Application Access

Once the application is running and the service is configured, it can be accessed through a web browser using the EC2 public IP address and the configured NodePort.

```text
http://<EC2-Public-IP>:<NodePort>
```

The EC2 security group and Kubernetes service must permit the required network traffic.

## Project Implementation Evidence

The following screenshots document the actual implementation and deployment process.

### 1. Jenkins Pipeline Execution

Shows the Jenkins pipeline stages and their execution results.

![Jenkins Pipeline Execution](screenshots/jenkins-build.png)

### 2. Maven Build and Testing

Evidence of the application's Maven build and testing process.

![Maven Build and Testing](screenshots/maven-build.png)

### 3. Docker Image

Shows the Docker image created for the application.

![Docker Image](screenshots/docker-image.png)

### 4. Docker Hub Repository

Shows the container image published to Docker Hub.

![Docker Hub Repository](screenshots/docker-hub.png)

### 5. Kubernetes Deployment

Shows the Kubernetes deployment configuration and deployment status.

![Kubernetes Deployment](screenshots/kubernetes-deployment.png)

### 6. Kubernetes Pods

Shows the status of the application's Kubernetes pods.

![Kubernetes Pods](screenshots/kubernetes-pods.png)

### 7. Kubernetes Service

Shows the Kubernetes service used to expose the application.

![Kubernetes Service](screenshots/kubernetes-service.png)

### 8. Application Output

Shows the deployed Spring Boot application running in the browser.

![Application Output](screenshots/application-browser.png)

> **Note:** Update the screenshot paths above to match the exact filenames in your `Screenshots` folder. Keep only the sections for screenshots you have uploaded.

## Application Output

After successful deployment, the application displays:

```text
Welcome to our DevOps Project !!
```

The application is accessed through the EC2 public IP address and the configured Kubernetes NodePort.

## Project Structure

```text
springboot-cicd-pipeline/
│
├── Images/
│   ├── project-architecture.jpeg
│   └── jenkins-pipeline.jpeg
│
├── Screenshots/
│   ├── jenkins-build.png
│   ├── maven-build.png
│   ├── docker-image.png
│   ├── docker-hub.png
│   ├── kubernetes-deployment.png
│   ├── kubernetes-pods.png
│   ├── kubernetes-service.png
│   └── application-browser.png
│
├── src/
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

*This is an illustrative structure. The actual filenames and directories should match the contents of your repository.*

## Key Learnings

Through this project, I gained practical experience in:

- Managing source code using GitHub.
- Automating CI/CD workflows with Jenkins.
- Building and testing Java applications using Maven.
- Creating and publishing Docker images.
- Using Docker Hub as a container image registry.
- Deploying containerized applications using Kubernetes.
- Working with AWS EC2 and Linux environments.
- Understanding the end-to-end CI/CD workflow.

## Future Improvements

- Configure and verify automated pipeline triggers using GitHub webhooks.
- Add pipeline failure notifications.
- Implement application monitoring and centralized logging.
- Introduce automated security scanning.
- Explore safer Kubernetes deployment strategies.


