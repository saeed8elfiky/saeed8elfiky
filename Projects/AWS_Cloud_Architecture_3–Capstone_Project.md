# AWS Cloud Architecture 3 – Capstone Project

## 📌 Overview
This project was developed as part of my AWS Cloud Architecture training.  
It focuses on migrating and redesigning a legacy research web application into a **secure, scalable, and highly available AWS architecture** that follows cloud best practices.

---

## 📝 Scenario
A nonprofit organization provides a website for social science researchers to access global development statistics (e.g., life expectancy by country).  

Originally:
- The app was hosted on a commercial hosting provider with limited security and support.  
- The website and MySQL database ran on the **same EC2 instance in a public subnet**.  
- Increasing traffic caused performance issues.  
- An attempted ransomware attack raised concerns about security.  

**Objective:** Redesign and migrate the application to AWS to improve **security, performance, and availability**.

---

## 💡 Solution Summary
The new AWS architecture ensures:  
- Secure hosting of the **MySQL database** with controlled access.  
- Anonymous access for web users via an **Application Load Balancer (ALB)**.  
- Website hosted on **EC2 instances in private subnets** (t2.micro).  
- Secure **SSH access for administrators** only.  
- **Auto Scaling Group** for elasticity and high availability.  
- Data stored in **Amazon RDS (MySQL)** with Secrets Manager integration.

<p align="center">
<img src="imgs/aws-arch-capstone.png" width="500">
</p>

---

## ⚙️ Implementation Steps

### 1. Amazon RDS (MySQL)
- Created RDS instance with `countries` database.  
- Credentials securely stored in **AWS Secrets Manager**.  
- Storage autoscaling enabled (20 GB).  
- Connected via private VPC security group.

### 2. Application Load Balancer (ALB)
- Internet-facing ALB named `AppELB`.  
- Target Group `ELB-TG` created to route traffic.  
- Deployed across **two Availability Zones** for redundancy.  
- Secured with **ALB Security Group**.

### 3. Auto Scaling Group (ASG)
- Launch Template (`Project-LT`) for EC2 instances.  
- EC2 instances deployed into **private subnets**.  
- Integrated with ALB target group.  
- Scaling policy:  
  - Min = 1 instance  
  - Max = 2 instances  

### 4. Database Configuration
- Connected to RDS using admin credentials from Secrets Manager.  
- Imported dataset (`Countrydatadump.sql`) into `countries` database.  
- Verified data availability via MySQL queries.

### 5. Testing
- Accessed the web app via **ALB DNS URL**.  
- Successfully queried development statistics by category.  
- Verified **load balancing and auto scaling** functionality.

---

## 🛠️ AWS Services Used
- **Amazon EC2** (Private subnets, Web application hosting)  
- **Amazon RDS (MySQL)** (Managed database)  
- **AWS Secrets Manager** (Credential storage)  
- **Application Load Balancer (ALB)**  
- **Auto Scaling Group (ASG)**  
- **VPC with Subnets (Public & Private)**  
- **Security Groups**  

---

## 🎯 Key Outcomes
- Migrated legacy application to a **secure, highly available AWS architecture**.  
- Improved **performance and scalability** with load balancing and auto scaling.  
- Enforced **security best practices**: private subnets, RDS isolation, Secrets Manager.  
- Gained hands-on experience in **end-to-end AWS solution design**.  

---

## 🙌 Acknowledgment
This capstone project was completed as part of my **AWS Cloud Architecture training**.
