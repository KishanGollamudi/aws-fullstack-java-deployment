# ☁️ AWS Full-Stack Infrastructure Deployment Project

This project demonstrates the complete setup of a production-style, scalable AWS environment from scratch using VPC networking, EC2 instances, NAT Gateway, RDS, and a Java web application running on Apache Tomcat. It includes secure routing, private-public subnetting, and a full database connection.

---

## 🔧 Project Architecture

### 🔹 VPC & Networking
- Created a custom **VPC** with a `/16` CIDR block.
- Configured **2 Public Subnets** and **2 Private Subnets** across two Availability Zones: `us-east-1a` and `us-east-1b`.
- Attached an **Internet Gateway** for public internet access.
- Created and associated **Route Tables** for public and private subnets.
- Configured a **NAT Gateway** in a public subnet to provide one-way internet access to private instances.

### 🔹 Compute Layer (EC2)
- Launched a **Public EC2 (Application Layer)** in AZ `1a`.
- Launched a **Private EC2 (Database Layer)** in AZ `1b`.
- Deployed a **Bastion Host** in the public subnet for SSH access to the private instance.
- Installed and configured **MySQL Server** on the private EC2 instance.

### 🔹 Database Layer (RDS)
- Provisioned an **Amazon RDS MySQL instance** in the private subnet.
- Secured RDS using proper **security groups**, subnet groups, and parameter groups.
- Verified private EC2 instance can connect and operate on RDS.

### 🔹 Application Layer (Java + Tomcat)
- Deployed another **EC2 instance** in a public subnet to run a **Java web app**.
- Installed **Apache Tomcat**, uploaded `.war` file.
- Java application supports:
  - Creating user accounts
  - Storing username and password in **MySQL DB**

---

## 🗺️ Architecture Diagram

<img width="972" height="811" alt="Image" src="https://github.com/user-attachments/assets/704f9503-c44f-48e9-b42a-083317bf917b" />

## 📄 Infrastructure as Code

This project uses AWS CloudFormation to provision all resources.

- [View CloudFormation Template](./cloudformation-template.yaml)

To deploy the stack:

```bash
aws cloudformation create-stack \
  --stack-name fullstack-java-app \
  --template-body file://cloudformation-template.yaml \
  --capabilities CAPABILITY_NAMED_IAM

---

### 🛑 Make Sure to:

- **Remove any hardcoded passwords, secrets, or keys** before uploading.
