A comprehensive demonstration of modern DevSecOps practices integrated into a 3-tier web application. This project showcases how to build secure, containerized applications with automated CI/CD pipelines, security scanning, and vulnerability management.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [CI/CD Pipeline](#cicd-pipeline)
- [Security Implementation](#security-implementation)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [Environment Configuration](#environment-configuration)
- [Troubleshooting](#troubleshooting)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Project Overview

This project demonstrates a complete DevSecOps workflow for a production-ready 3-tier web application. It follows industry best practices by integrating security at every stage of the development lifecycle, from source code to container deployment.

### Application Structure

The application is organized into three main components:

- **Frontend**: A responsive web interface built with React and Vite that provides an intuitive user experience
- **Backend**: A Node.js-based REST API using Express.js that handles business logic, data processing, and service orchestration
- **Database**: A persistent data layer for storing application data
- **Infrastructure**: Fully containerized using Docker and Docker Compose for environment consistency

## 🛠 Technology Stack

### Frontend
- **React** - UI library for building interactive components
- **Vite** - Next-generation build tool for fast development and optimized production builds
- **CSS** - Styling and responsive design

### Backend
- **Node.js** - JavaScript runtime for server-side development
- **Express.js** - Web framework for building REST APIs
- **Docker** - Containerization platform

### DevOps & Security
- **Docker & Docker Compose** - Containerization and orchestration
- **GitHub Actions** - CI/CD automation
- **Trivy** - Container image vulnerability scanning
- **Shell Scripts** - Infrastructure automation

### Languages Used
- JavaScript: 49.9%
- CSS: 44.7%
- HTML: 3.2%
- Dockerfile: 2.2%

## 🏗 Architecture

```
┌─────────────────────────────────────────────┐
│           Internet / Users                   │
└────────────────┬────────────────────────────┘
                 │
        ┌────────▼─────────┐
        │   Frontend       │
        │ (React + Vite)   │
        │  Port: 3000      │
        └────────┬─────────┘
                 │ HTTP/REST
        ┌────────▼─────────┐
        │   Backend API    │
        │  (Express.js)    │
        │  Port: 5000      │
        └────────┬─────────┘
                 │
        ┌────────▼─────────┐
        │    Database      │
        │  (Persistent)    │
        └──────────────────┘
```

## 🚀 Getting Started

### Prerequisites

- Docker (version 20.10 or later)
- Docker Compose (version 1.29 or later)
- Node.js 16+ (optional, for local development)
- Git

### Installation & Running

1. **Clone the repository**
   ```bash
   git clone https://github.com/Satwikvarma/devsecops-3tier-app.git
   cd devsecops-3tier-app
   ```

2. **Start the application using Docker Compose**
   ```bash
   docker compose up --build
   ```

3. **Access the services**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000
   - API Health Check: http://localhost:5000/health

4. **Stop the application**
   ```bash
   docker compose down
   ```

### Local Development (Without Docker)

#### Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

#### Backend Setup
```bash
cd backend
npm install
npm start
```

## 🔄 CI/CD Pipeline

### Workflow Overview

The GitHub Actions CI/CD pipeline automatically triggers on every push to the main branch and performs comprehensive build, test, and security validation.

### Pipeline Stages

1. **Source Code Checkout**
   - Fetches the latest code from the repository

2. **Dependency Installation**
   - Installs frontend dependencies (Node.js packages)
   - Installs backend dependencies (Node.js packages)

3. **Code Quality Checks**
   - Linting and code style validation
   - Building frontend and backend applications

4. **Docker Image Build**
   - Builds containerized images for frontend and backend
   - Tags images with commit SHA and latest tags

5. **Security Scanning**
   - Trivy scans Docker images for known vulnerabilities
   - Detects exposed secrets and misconfigurations
   - Generates security reports

6. **Vulnerability Assessment**
   - Evaluates severity levels (Critical, High, Medium, Low)
   - Fails the pipeline on Critical or High severity findings
   - Provides detailed remediation guidance

### Pipeline Configuration

The GitHub Actions workflow is configured in:
```
.github/workflows/ci.yml
```

**Key Features:**
- Automatic triggering on push events
- Parallel job execution for efficiency
- Artifact storage for build outputs
- Detailed logs for debugging and audit trails

## 🔒 Security Implementation

### Security-First Approach

Security is not an afterthought but is integrated directly into the development workflow:

### Security Measures

1. **Container Image Scanning**
   - Trivy scans all Docker images before deployment
   - Identifies vulnerable dependencies and system libraries
   - Checks for exposed secrets and credentials

2. **Vulnerability Management**
   - Pipeline fails on Critical or High severity vulnerabilities
   - Early detection prevents insecure code from progressing
   - Automatic notifications on security findings

3. **Secret Detection**
   - Scans for accidentally committed credentials
   - Prevents exposure of API keys and tokens
   - Enforces secret management best practices

4. **Base Image Selection**
   - Uses minimal, security-hardened base images
   - Regular updates to patch known vulnerabilities
   - Documented inventory of all dependencies

### Security Best Practices

- Use environment variables for sensitive configuration
- Never commit secrets or credentials
- Regularly update dependencies
- Review security scanning reports
- Implement proper access controls

## 📁 Project Structure

```
devsecops-3tier-app/
├── frontend/                    # React + Vite application
│   ├── src/
│   │   ├── components/         # React components
│   │   ├── pages/              # Page components
│   │   └── styles/             # CSS styling
│   ├── Dockerfile              # Frontend container definition
│   ├── package.json            # Frontend dependencies
│   └── vite.config.js          # Vite configuration
├��─ backend/                     # Express.js API server
│   ├── routes/                 # API route definitions
│   ├── controllers/            # Business logic handlers
│   ├── models/                 # Data models
│   ├── Dockerfile              # Backend container definition
│   ├── package.json            # Backend dependencies
│   └── server.js               # Entry point
├── .github/
│   └── workflows/
│       └── ci.yml              # GitHub Actions CI/CD pipeline
├── docker-compose.yml          # Multi-container orchestration
└── README.md                    # This file
```

## 🔌 API Endpoints

### Health Check
```
GET /health
```
Response: `{ "status": "healthy" }`

### Base URL
```
http://localhost:5000/api
```

### Available Endpoints
- `GET /api/data` - Retrieve application data
- `POST /api/data` - Create new data entry
- `GET /api/data/:id` - Retrieve specific data
- `PUT /api/data/:id` - Update data entry
- `DELETE /api/data/:id` - Delete data entry

## ⚙️ Environment Configuration

Create a `.env` file in the root directory for environment-specific configuration:

```env
# Frontend
VITE_API_URL=http://localhost:5000/api
VITE_APP_NAME=DevSecOps 3-Tier App

# Backend
NODE_ENV=development
PORT=5000
DB_HOST=db
DB_PORT=5432
DB_NAME=appdb
DB_USER=postgres
DB_PASSWORD=postgres

# Security
ENABLE_HTTPS=false
LOG_LEVEL=debug
```

## 🔧 Troubleshooting

### Container won't start
```bash
# Check logs
docker compose logs -f

# Rebuild containers
docker compose down
docker compose up --build
```

### Port already in use
```bash
# Change ports in docker-compose.yml or stop conflicting services
docker ps
docker stop <container-id>
```

### Dependency issues
```bash
# Clean and reinstall dependencies
docker compose down --volumes
docker compose up --build
```

### Pipeline failures
- Check GitHub Actions logs in the repository
- Verify all environment variables are set correctly
- Ensure Docker images are properly built and pushed
- Review Trivy security scanning reports for vulnerabilities

## 🚀 Future Enhancements

### Infrastructure & Scaling
- [ ] Kubernetes deployment configuration for production scaling
- [ ] Helm charts for simplified K8s deployments
- [ ] Load balancing and auto-scaling policies
- [ ] Multi-region deployment strategy

### Code Quality & Testing
- [ ] SonarQube integration for static code analysis
- [ ] Comprehensive unit and integration test suites
- [ ] Code coverage reporting and enforcement
- [ ] Performance benchmarking and profiling

### Deployment & Operations
- [ ] Automated deployment pipeline to AWS/Azure/GCP
- [ ] Infrastructure as Code (Terraform/CloudFormation)
- [ ] Blue-green deployment strategy
- [ ] Canary release automation

### Monitoring & Observability
- [ ] Prometheus for metrics collection
- [ ] Grafana for visualization and dashboards
- [ ] ELK Stack for centralized logging
- [ ] Distributed tracing with Jaeger
- [ ] Alerting and incident management

### Security Enhancements
- [ ] OWASP dependency checking
- [ ] DAST (Dynamic Application Security Testing)
- [ ] Container registry scanning
- [ ] Runtime security monitoring

## 👥 Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📞 Support & Questions

For issues, questions, or suggestions, please:
- Open an issue on GitHub
- Check existing issues and discussions
- Review the troubleshooting section above

---

**Last Updated**: 2026-06-04
**Project Status**: Active Development
