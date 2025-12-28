# Jenkins CI/CD Flask Application 🚀

A modern Flask web application featuring a complete CI/CD pipeline with Jenkins, fully containerized with Docker for seamless development and deployment.

## 🐳 Docker Architecture

This project leverages Docker to ensure consistent environments across development, testing, and production: 

- **Base Image**: Python 3.13.0a2 on Alpine Linux for minimal footprint
- **Lightweight**:  Alpine-based image reduces container size significantly
- **Security**: Runs as non-root user (`myuser`) following security best practices
- **Cloud-Ready**: Configured for Heroku deployment with dynamic port binding

## ✨ Features

- 🔄 **Automated CI/CD**:  Jenkins pipeline for continuous integration and deployment
- 🐳 **Dockerized**:  Fully containerized application for portability
- 🧪 **Testing Ready**: Integrated testing framework in CI/CD pipeline
- ☁️ **Cloud Deployment**: Heroku-ready configuration
- 🔒 **Security Focused**: Non-root user execution in container
- ⚡ **Performance**:  Gunicorn WSGI server for production-grade performance

## 📋 Prerequisites

- Docker Desktop or Docker Engine
- Git
- Jenkins (for CI/CD pipeline)
- Heroku CLI (optional, for deployment)

## 🚀 Quick Start with Docker

### 1. Clone the repository

```bash
git clone https://github.com/AnselmeG300/jenkins-CICD-flask-app.git
cd jenkins-CICD-flask-app
```

### 2. Build the Docker image

```bash
docker build -t flask-cicd-app .
```

### 3. Run the container

```bash
docker run -p 5000:5000 -e PORT=5000 flask-cicd-app
```

### 4. Access the application

Open your browser and navigate to:  `http://localhost:5000`

## 🏗️ Project Structure

```
jenkins-CICD-flask-app/
├── Dockerfile              # Docker configuration
├── webapp/
│   ├── requirements.txt    # Python dependencies
│   ├── wsgi.py            # WSGI entry point
│   └── ...                 # Flask application files
├── Jenkinsfile            # CI/CD pipeline configuration
└── README.md
```

## 🐳 Dockerfile Breakdown

```dockerfile
# Lightweight Alpine-based Python image
FROM python:3.13.0a2-alpine

# Essential tools installation
RUN apk add --no-cache --update python3 py3-pip bash

# Dependency installation
ADD ./webapp/requirements.txt /tmp/requirements.txt
RUN pip3 install --no-cache-dir -q -r /tmp/requirements.txt

# Application code
ADD ./webapp /opt/webapp/
WORKDIR /opt/webapp

# Security:  Non-root user
RUN adduser -D myuser
USER myuser

# Gunicorn server with dynamic port
CMD gunicorn --bind 0.0.0.0:$PORT wsgi
```

## 🔧 Configuration

### Environment Variables

- `PORT`: Application port (set automatically by Heroku, or manually for local development)

### Dependencies

All Python dependencies are listed in `webapp/requirements.txt`:
- Flask
- Gunicorn
- (other dependencies...)

## 🚢 Deployment

### Heroku Deployment

```bash
# Login to Heroku
heroku login

# Create a new Heroku app
heroku create your-app-name

# Deploy using Docker
heroku container:push web
heroku container:release web

# Open your app
heroku open
```

## 🔄 CI/CD Pipeline

The Jenkins pipeline automates: 

1. **Code Checkout**: Pull latest code from repository
2. **Build**:  Create Docker image
3. **Test**:  Run automated tests
4. **Deploy**: Push to production (Heroku)

## 🛠️ Development

### Local Development (without Docker)

```bash
cd webapp
pip install -r requirements. txt
export PORT=5000
python wsgi.py
```

### Local Development (with Docker)

```bash
# Build
docker build -t flask-app-dev .

# Run with volume mounting for live reload
docker run -p 5000:5000 -e PORT=5000 \
  -v $(pwd)/webapp:/opt/webapp \
  flask-app-dev
```

## 🧪 Testing

```bash
# Run tests in Docker container
docker run flask-cicd-app pytest

# Or locally
cd webapp
pytest
```

## 📝 Best Practices Implemented

- ✅ Multi-stage builds consideration for size optimization
- ✅ Non-root user execution for security
- ✅ No-cache pip installation to reduce image size
- ✅ Alpine Linux for minimal attack surface
- ✅ Environment-based configuration
- ✅ Gunicorn for production-ready WSGI server

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

**AnselmeG300**

- GitHub: [@AnselmeG300](https://github.com/AnselmeG300)

## 🙏 Acknowledgments

- Jenkins for CI/CD automation
- Docker for containerization
- Heroku for cloud deployment
- Flask framework community

---

⭐ Star this repository if you find it helpful! 
```
