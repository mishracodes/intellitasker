# IntelliTasker – AI-Powered Task Automation SaaS

**IntelliTasker** is a cloud-native, multi-user SaaS platform designed to automate recurring tasks, manage files, send alerts, and track workflows — all built using AWS services and DevOps best practices.

## 🔧 Architecture Overview

- **Frontend**: HTML/Bootstrap (or React later)
- **Backend**: Python (Flask or FastAPI)
- **Database**: Amazon RDS (PostgreSQL), DynamoDB
- **File Storage**: Amazon S3 + Glacier for backups
- **Authentication**: Amazon Cognito
- **CI/CD**: GitHub → CodePipeline → CodeBuild → EC2
- **Task Automation**: Lambda, EventBridge, Step Functions
- **Monitoring**: CloudWatch, SNS, X-Ray
- **Infrastructure**: CloudFormation / Terraform

## 🚀 Project Goal

To provide a modular, extensible system for users to create and run intelligent task workflows, and in the process, gain deep hands-on experience with AWS, CI/CD, Git, and full-stack DevOps.

---
