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
```

## 📸 CIDR-Screenshots
VPC CIDR Calculation
<img width="1275" height="795" alt="Image" src="https://github.com/user-attachments/assets/f4dcab8d-a61c-4b77-b992-c15a4b6009a3" />
Subnet 1a CIDR
<img width="1439" height="803" alt="Image" src="https://github.com/user-attachments/assets/caa04813-8b8d-4803-8ee1-c393e9f934e4" />
Subnet 1b CIDR
<img width="1369" height="772" alt="Image" src="https://github.com/user-attachments/assets/274f6d5e-0f12-4e97-80e8-87b0a755b791" />

## 📸 Screenshots
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/58eb2efa-5fd1-462b-a6b3-a7650f775931" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/499edfdf-5771-4734-8805-2f6ce61083bf" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/3a48abf4-07ba-45b6-bdda-03d0253e3740" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/14612446-2ee9-4192-88c8-665047e620a1" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/efd2f391-61ad-4593-bcab-e88dc4d49b85" />

<img width="1590" height="433" alt="Image" src="https://github.com/user-attachments/assets/58edd0a8-c69d-4122-bcec-3e9edffc8226" />

<img width="610" height="948" alt="Image" src="https://github.com/user-attachments/assets/bdeb1b78-ba12-4d78-b0c1-757466b0c41d" />

<img width="945" height="499" alt="Image" src="https://github.com/user-attachments/assets/b00a2832-db9f-4255-a263-aad4afc1154a" />

<img width="1243" height="907" alt="Image" src="https://github.com/user-attachments/assets/0fc284cf-5d9c-42c1-a852-5164defa7230" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/b225fe22-1221-4d56-9c0e-0efd2c13427b" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/c3cc1e18-8e1f-4d66-ad0a-105456d34e33" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/6955e6c9-f766-4a25-979d-c61791f69f42" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/6aaed846-17bd-4b82-bfbf-6fc2333a26b0" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/1b4bbdd1-6dc7-4523-b1f9-3af0a3cfa174" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/9d21c55a-c798-4542-a78c-4151cede0344" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/a8a85d4b-d6cf-4f70-abac-6d26dbe93fa6" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/5e34197a-3539-448b-8607-628d2b587458" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/4e0b8384-7270-4757-afec-927bbcd7a02f" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/b11bf185-d919-48a7-9869-d3571db50c53" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/ca66b389-6284-4fdb-b16f-7320b6def348" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/6914150f-f2ea-46b5-a17b-b7895f80a93f" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/da58a7e6-2d2a-4792-ae54-1430791346d9" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/4dca83b1-a4ee-49e0-bd62-457c5c508a0d" />

