# AWS DevSecOps CI/CD Pipeline with Terraform

This project implements a complete **DevSecOps CI/CD pipeline** on AWS for a Java WAR-based application. It uses **Terraform** to provision and manage the entire infrastructure in a modular, reusable way. The setup integrates static code analysis, software composition analysis, and automated deployments using AWS services.

---

## 🚀 Project Objectives

- Automate build, test, and deploy steps for a Java web application
- Integrate DevSecOps security practices at every stage
- Use Terraform to manage all AWS resources and infrastructure
- Keep the architecture within AWS Free Tier (where possible)
- Allow future scalability into production-grade pipelines

---

## 🧰 Tech Stack

| Layer         | Tool/Service                |
|--------------|-----------------------------|
| IaC          | Terraform                   |
| CI/CD        | AWS CodePipeline            |
| Build/Test   | AWS CodeBuild + Maven       |
| App Runtime  | AWS Elastic Beanstalk       |
| Storage      | Amazon S3                   |
| Security     | IAM, SNS, SonarCloud, OWASP |
| Source Repo  | GitHub                      |

---

## 🏗️ Architecture

```plaintext
GitHub → CodePipeline
         ├── Source Stage (CodeStar Connection)
         ├── Build Stage (CodeBuild)
         │     ├── Maven Build (ROOT.war)
         │     ├── JaCoCo Code Coverage
         │     ├── OWASP Dependency Check (SCA)
         │     ├── SonarCloud Scan (SAST)
         │     ├── Upload Reports to S3
         │     └── SNS Notifications (with presigned URLs)
         └── Deploy Stage (Elastic Beanstalk - Staging)


## Terraform Project Structure

.
├── main.tf
├── variables.tf
├── terraform.tfvars
├── outputs.tf
└── modules/
    ├── iam/
    ├── s3/
    ├── elastic_beanstalk/
    ├── codebuild/
    └── codepipeline/
