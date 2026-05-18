# ☁️ Cloud Network Security Deployment (Sec-Cloud – Pharma Link Logistics)

**Author:** Sara Amjad | **Date:** May 2026  
> **Academic Context:**  
This project was developed as part of **Unit 23: Applied Security in the Cloud** under the **Pearson BTEC HND in Digital Technologies (Cyber Security)**. The system demonstrates the design, deployment, and evaluation of cloud network security solutions for a simulated AWS-hosted SQL environment of *Pharma Link Logistics*, focusing on role-based access control, data encryption, auditing mechanisms, automated backups, and cloud monitoring strategies to ensure secure, scalable, and resilient cloud infrastructure.
## 📌 Project Overview
This project demonstrates the implementation of a secure AWS RDS-based SQL database for a simulated organization. The system focuses on strengthening cloud security using role-based access control, AES encryption, auditing mechanisms, automated backups, and cloud monitoring.

## 🏗️ Security Implementation Overview

The system is structured into four key security layers:

- 🔐 Role-Based Access Control (RBAC)
- 🛡️ Data Encryption using AES
- 📜 Audit Logging and Activity Tracking
- ☁️ Cloud Monitoring and Backup (AWS)

## 🔐 1. Role-Based Access Control (RBAC)

Database access was restricted using predefined roles and SQL GRANT permissions.

<p align="center">
  <img src="Images/Query Applied for Creating Roles.png" width="600"/>
</p>

<p align="center">
  <img src="Images/GRANT Queries Applied to the Roles .png" width="700"/>
</p>

<p align="center">
  <img src="Images/Users Created After Queries (1) .png" width="700"/>
</p>

<p align="center">
  <img src="Images/Users Created After Queries (2) .png" width="700"/>
</p>

## 🛡️ 2. AES Data Encryption
Sensitive data fields were encrypted using AES functions to ensure confidentiality.

<p align="center">
  <img src="Images/Encryption Query Applied to Sensitive Table Columns .png" width="700"/>
</p>

<p align="center">
  <img src="Images/Queries Applied for Creation of Decrypted View .png" width="700"/>
</p>

<p align="center">
  <img src="Images/Alter Query Applied for Encrypting Sensitive Columns .png" width="600"/>
</p>

## 📜 3. Audit Logging System
All database activities were recorded using a centralized logging mechanism.

<p align="center">
  <img src="Images/Result Log Table .png" width="700"/>
</p>

<p align="center">
  <img src="Images/AWS RDS Automated Logs .png" width="700"/>
</p>

## 🧪 4. Benchmark & Verification Testing
Security controls were tested to ensure correctness and performance.

<p align="center">
  <img src="Images/Reply to Pharma User .png" width="700"/>
</p>

<p align="center">
  <img src="Images/Decrypted View of Pharmacies Table for Admins Only .png" width="700"/>
</p>

## ☁️ 5. Cloud Monitoring (AWS)
AWS services were used for real-time monitoring and activity tracking.

<p align="center">
  <img src="Images/Cloud Watch Metrics of Pharma Link .png" width="700"/>
</p>

<p align="center">
  <img src="Images/Implementation of Cloud Trail .png" width="700"/>
</p>

## 💾 6. Backup & Recovery
AWS RDS backups and snapshots were configured for system resilience.

<p align="center">
  <img src="Images/RDS Snapshots of Database .png" width="900"/>
</p>

## ⚙️ Tools & Technologies Used

- AWS RDS (MySQL Database)  
- AWS CloudWatch  
- AWS CloudTrail  
- SQL (RBAC, GRANT, Queries)  
- AES Encryption Functions  
- Database Auditing System

## ⚠️ Disclaimer
This repository was developed for academic and educational purposes to demonstrate the implementation of cloud network security solutions within a functionally implemented AWS-based SQL environment.All security configurations, database structures, encryption methods, monitoring systems, audit logs, and backup mechanisms presented in this project were implemented in a simulated AWS cloud setup using SQL and AWS services (RDS, CloudWatch, and CloudTrail). However, the system is not deployed as a real production environment and does not process live organizational data.This project is intended solely for learning, demonstration, and portfolio purposes.
