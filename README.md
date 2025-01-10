# Creating the markdown file for the user

doc_content = """
# I-Recharge Application Documentation

## 📋 Table of Contents
1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Prerequisites](#prerequisites)
4. [Setup Instructions](#setup-instructions)
5. [Infrastructure Overview (Terraform)](#infrastructure-overview-terraform)
6. [CI/CD Pipeline (GitHub Actions)](#cicd-pipeline-github-actions)
7. [Environment Variables](#environment-variables)
8. [Connecting to RDS Database](#connecting-to-rds-database)
9. [Contributing](#contributing)
10. [License](#license)

---

## 🚀 Project Overview

The **I-Recharge Application** is a web-based platform designed for high availability, scalability, and security. It utilizes AWS services for cloud infrastructure and Docker for containerization. The project is automated with a CI/CD pipeline using GitHub Actions to streamline the build, test, and deployment processes to AWS.

---

## 🏗️ Architecture

The infrastructure for the I-Recharge application is deployed using **Terraform**, utilizing the following AWS services:

- **Amazon EC2**: To run the application container.
- **Amazon RDS (PostgreSQL)**: For the application’s database.
- **Amazon ECR**: A private container registry for storing Docker images.
- **AWS Secrets Manager**: For securely managing database credentials.
- **AWS IAM**: For managing access permissions.

---

## ⚙️ Prerequisites

Before setting up the I-Recharge application, ensure you have the following tools installed on your local machine:

- **Terraform**
- **AWS CLI**
- **Docker**
- **Node.js**

---

## 🛠️ Setup Instructions

Follow these steps to set up the I-Recharge application:

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/your-repo/i-recharge.git
cd i-recharge
