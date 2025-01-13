
# I-Recharge Task

This project is a cloud-based application that leverages AWS infrastructure, Docker, and a CI/CD pipeline using GitHub Actions for seamless deployment. The app includes an Amazon RDS database, Amazon ECR for container storage, and automated deployment to AWS.

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
- [Infrastructure Overview (Terraform)](#infrastructure-overview-terraform)
- [CI/CD Pipeline (GitHub Actions)](#cicd-pipeline-github-actions)
- [Environment Variables](#environment-variables)
- [Contributing](#contributing)
- [License](#license)

## 🚀 Project Overview

The I-Recharge Application is a web-based platform designed to be highly available, scalable, and secure. It uses AWS services for cloud infrastructure and Docker for containerization. The project is automated with a CI/CD pipeline using GitHub Actions to build, test, and deploy the application to AWS.

## 🏗️ Architecture

The infrastructure is deployed using Terraform and includes the following AWS services:

- **Amazon EC2**: For running the application container.
- **Amazon RDS**: A PostgreSQL database instance.
- **Amazon ECR**: A private container registry for storing Docker images.
- **AWS Secrets Manager**: For securely managing database credentials.
- **AWS IAM**: For managing access permissions.

## ⚙️ Prerequisites

Ensure you have the following installed on your local machine:

- Terraform
- AWS CLI
- Docker
- Node.js

## 🛠️ Setup Instructions

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/ShepherdPraise/i-recharge.git
cd i-recharge
```

### 2️⃣ Configure AWS CLI

Make sure your AWS CLI is configured with appropriate access credentials.

```bash
aws configure
```

### 3️⃣ Build and Run the Application Locally

```bash
docker build -t i-recharge-app .
docker run -p 8080:8080 i-recharge-app
```

The app will be accessible at [http://localhost:8080](http://localhost:8080).

## 📦 Infrastructure Overview (Terraform)

The project uses Terraform to provision AWS resources. The infrastructure includes:

- EC2 Instance for running the app container.
- RDS (PostgreSQL) for the database.
- Secrets Manager for storing credentials.
- ECR for storing Docker images.

### 📄 Terraform Commands

#### Initialize Terraform:

```bash
terraform init
```

#### Review the changes:

```bash
terraform plan
```

#### Apply the changes:

```bash
terraform apply
```

## 🔄 CI/CD Pipeline (GitHub Actions)

The project uses GitHub Actions for CI/CD. The workflow automates:

- Building the Docker image
- Pushing the image to Amazon ECR
- Deploying the container to an AWS EC2 instance

### GitHub Actions Workflow File

```yaml
name: Build and Deploy to AWS

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Login to Amazon ECR
        id: ecr-login
        uses: aws-actions/amazon-ecr-login@v1

      - name: Build Docker Image
        run: |
          docker build -t $ECR_REPO_NAME:latest .

      - name: Push to ECR
        run: |
          docker push ${{ env.AWS_ACCOUNT_ID }}.dkr.ecr.${{ env.AWS_REGION }}.amazonaws.com/$ECR_REPO_NAME:latest
```

## 🔑 Environment Variables

The following environment variables are required for the application:

| Variable              | Description                             |
|-----------------------|-----------------------------------------|
| `DB_HOST`             | The RDS instance endpoint               |
| `DB_PORT`             | The database port (5432)                |
| `DB_USERNAME`         | The database username                   |
| `DB_PASSWORD`         | The database password                   |
| `AWS_ACCESS_KEY_ID`   | AWS Access Key ID                       |
| `AWS_SECRET_ACCESS_KEY` | AWS Secret Access Key                  |
| `ECR_REPO_NAME`       | Name of the Amazon ECR repo             |

## 💻 Connecting to RDS Database

To connect to your RDS instance, use a tool like pgAdmin or DBeaver.  
Use the `DB_HOST`, `DB_PORT`, `DB_USERNAME`, and `DB_PASSWORD` environment variables for the connection.

## 🤝 Contributing

We welcome contributions to the I-Recharge project! Feel free to submit issues or pull requests on GitHub.

### Steps to Contribute:
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push the branch
5. Create a pull request
