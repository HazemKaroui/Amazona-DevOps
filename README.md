# Amazon clone Deployment with Docker, Kubernetes, and Jenkins
By *Ilhem Elmissaoui* & *Hazem Karoui*

## Introduction

The project is a modern web application built with React for the front-end, Node.js for the back-end, and MongoDB as the database. The deployment is orchestrated using Docker containers, and the continuous integration and deployment (CI/CD) process is managed through Jenkins. Kubernetes is employed for container orchestration and scaling.

## Components

### Frontend

The frontend of the application is developed using React, a popular JavaScript library for building user interfaces. It provides a dynamic and responsive user experience.

### Backend

The backend of the application is powered by Node.js, offering a scalable and efficient server-side runtime. It interacts with the MongoDB database to retrieve and update data.

### Database

MongoDB, a NoSQL database, is utilized for storing and managing data in a flexible and scalable manner.

## Technologies Used

- **Frontend:** React
- **Backend:** Node.js
- **Database:** MongoDB
- **Containerization:** Docker
- **Container Orchestration:** Kubernetes
- **CI/CD:** Jenkins

## Project Structure

The project follows a microservices architecture, with each component residing in its own Docker container. This allows for modularity, scalability, and easy deployment across different environments.

## CI/CD Pipeline

Jenkins is configured to automate the CI/CD pipeline. The pipeline includes steps for code retrieval from the source repository, building Docker images, pushing images to Docker Hub.

## How to Use

## How to Use

Follow these steps to set up the development environment, configure Docker Compose, and deploy the application using Kubernetes and Jenkins.

### 1. Prerequisites

Make sure you have the following prerequisites installed on your system:

- Docker
- Docker Compose
- Kubernetes (kubectl)
- Jenkins

### 2. Setting up the Kubernetes Cluster

Before deploying the application, ensure that you have a Kubernetes cluster available. If you don't have one, you can use tools like Minikube or set up a cluster on a cloud provider such as Google Kubernetes Engine (GKE) or Amazon EKS.

### 3. Configuring Docker Compose

1. Clone the project repository to your local machine:

    ```bash
    git clone https://github.com/HazemKaroui/Amazona-DevOps.git
    ```

2. Navigate to the project directory:

    ```bash
    cd Amazona-DevOps
    ```

3. Customize the Docker Compose file (`docker-compose.yml`) if necessary. Update environment variables, service names, or ports based on your requirements.

4. Build and start the Docker containers:

    ```bash
    docker-compose up -d
    ```

### 4. Setting up Jenkins

1. Install Jenkins on your preferred environment. You can follow the official Jenkins installation guide for your system.

2. Access the Jenkins dashboard and install necessary plugins, including the Docker and Kubernetes plugins.

3. Configure Jenkins to connect to your version control system (GitHub/GitLab) and set up a new pipeline project.

4. In the Jenkins pipeline configuration, define the necessary environment variables and credentials for Docker Hub and your Kubernetes cluster.

5. Save the pipeline configuration and trigger a build to initiate the CI/CD process.

### 5. Accessing the Application

Once the CI/CD pipeline is complete, access the deployed application using the external IP address or domain provided by your Kubernetes cluster. You can find the IP address by running:

```bash
kubectl get service frontend-service
```

## Cleanup

When you're finished testing the application, clean up the resources by running:

bash

```bash
docker-compose down
kubectl delete deployment frontend-deployment backend-deployment
kubectl delete service frontend-service backend-service
```
