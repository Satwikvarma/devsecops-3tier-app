# DevSecOps 3-Tier Web Application

This project demonstrates a complete DevSecOps workflow for a 3-tier web application. It follows a standard industry architecture with a frontend, backend, and database layer, and integrates CI/CD with security scanning using GitHub Actions.

## Project Overview

The application is structured into three main components:

Frontend: A web interface that interacts with users and communicates with the backend.

Backend: A Node.js-based API that handles business logic and data processing.

Database: Stores application data persistently.

The entire system is containerized using Docker to ensure consistency across environments.

## Technology Stack

Node.js for backend development  
Express.js for API handling  
Docker and Docker Compose for containerization  
GitHub Actions for CI/CD automation  
Trivy for security and vulnerability scanning  

## CI/CD Pipeline

The CI pipeline runs automatically on every push to the main branch. It performs the following steps:

- Source code checkout  
- Installation of frontend and backend dependencies  
- Docker image build process  
- Security scanning of container images using Trivy  
- Validation of vulnerabilities before allowing pipeline completion  

This ensures that only secure and buildable code progresses through the pipeline.

## Security Implementation

Security is integrated directly into the development workflow.

Trivy is used to scan Docker images for known vulnerabilities and exposed secrets. The pipeline is configured to fail if critical or high severity issues are detected, ensuring early detection of security risks.

## How to Run the Project

Clone the repository

git clone <repository-url>  
cd project-directory  

Start the application using Docker Compose

docker compose up --build  

Once running, the services can be accessed locally through the configured ports for frontend and backend.

## CI Configuration

The GitHub Actions workflow file is located at:

.github/workflows/ci.yml

It defines the complete build, test, and security scanning process.

## Future Enhancements

Kubernetes deployment for scalability  
Integration of SonarQube for code quality analysis  
Automated deployment pipeline to cloud platforms such as AWS  
Monitoring and logging using Prometheus and Grafana  

## Purpose of the Project

The goal of this project is to demonstrate how security can be integrated into a modern CI/CD pipeline while maintaining a simple microservice-based architecture. It reflects a practical DevSecOps approach used in real-world software engineering environments.
