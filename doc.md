
# Full Stack 

---

## Author Information

| **Created by** | **Created on** | **Version** | **Last Updated On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
|----------------|----------------|-------------|----------------------|------------------|-----------------|-----------------|-----------------|
| Sonal          | 30-07-2025     | V 1.0        | 30-07-2025           | Anjali           |                 |                 |                 |

---

## Table of Contents

1. [Introduction](#1-introduction)  
2. [Overview](#2-overview)  
3. [System Architecture](#3-system-architecture)  
4. [Pre-Requisites](#4-pre-requisites)  
5. [Dependencies](#5-dependencies)  
6. [Important Ports](#6-important-ports)  
7. [Setup Instructions](#7-setup-instructions)  
8. [Data Flow](#8-data-flow)  
9. [Troubleshooting](#9-troubleshooting)  
10. [Conclusion](#10-conclusion)  
11. [Contact Information](#11-contact-information)  
12. [References](#12-references)
---

## 1. Introduction

This document provides a comprehensive guide to deploying and managing a full-stack composed of four microservices:

- **Employee Management**
- **Attendance Tracking**
- **Salary Calculation**
- **Notification Handling**

The system is built using Go, Python (Flask), Java (Spring Boot), Redis, PostgreSQL, ScyllaDB, and Traefik. The architecture is based on microservices to ensure modularity, scalability, and independent deployments.

---

## 2. Overview

| **Microservice**             | **Language**        | **Database**           | **Queue/Cache** | **Purpose**                                                 | **Repository** |
|------------------------------|---------------------|-------------------------|------------------|--------------------------------------------------------------|----------------|
| **`employee-api`**           | Go                  | ScyllaDB                | Redis            | Manage employee records (CRUD)                              | [Link](https://github.com/OT-MICROSERVICES/employee-api) |
| **`attendance-api`**         | Python (Flask)      | PostgreSQL / MySQL      | Redis            | Record attendance, check-in/check-out, reports              | [Link](https://github.com/OT-MICROSERVICES/attendance-api) |
| **`salary-api`**             | Java (Spring Boot)  | MySQL / Elasticsearch   | Redis Queue      | Calculate salaries based on attendance, rules               | [Link](https://github.com/OT-MICROSERVICES/salary-api) |
| **`notification-worker`**    | Python              | N/A                     | Redis Queue      | Queue and send notifications via email/SMS                  | [Link](https://github.com/OT-MICROSERVICES/notification-worker) |
| **`Frontend` (optional)**    | React + Traefik     | N/A                     | N/A              | Interface to interact with backend services                               |[frontend](https://github.com/OT-MICROSERVICES/frontend) |

---

## 3. System Architecture

```plaintext
[Frontend (React)]
       |
    [Traefik]
       ↓
 ┌────────────┐      ┌──────────────┐      ┌─────────────┐      ┌──────────────────┐
 │employee-api│<──→──│attendance-api│<──→──│  salary-api │<───→─│notification-worker│
 └────────────┘      └──────────────┘      └─────────────┘      └──────────────────┘
       ↓                   ↓                       ↓                      ↓
   [ScyllaDB]        [PostgreSQL]            [MySQL/Elastic]          [SMTP/SMS]
       ↑                   ↑                       ↑                      ↑
     [Redis]           [Redis]                 [Redis Queue]          [Redis Queue]
````

---

## 4. Pre-Requisites

| **Requirement** | **Details**                      |
| --------------- | -------------------------------- |
| OS              | Ubuntu 22.04 / CentOS 8+         |
| CPU             | Quad-core recommended            |
| RAM             | Minimum 8 GB                     |
| Disk            | 40 GB free space                 |
| Network         | Ports 8080–8085, 5432, 6379 open |
| Security        | SSL/TLS, firewalled DB & Redis   |

---

## 5. Dependencies

### A. **Build-Time Tools**

| **Tool** | **Version** | **Used For**                                    |
| -------- | ----------- | ----------------------------------------------- |
| Python   | 3.11+       | **`attendance-api`**, **`notification-worker`** |
| Go       | 1.20+       | **`employee-api`**                              |
| Java     | 17+         | **`salary-api`**                                |
| pip/npm  | Latest      | Python & React dependencies                     |


### B. **Runtime Dependencies**

| **Service**               | **Libraries/Tools Used**       |
| ------------------------- | ------------------------------ |
| **`employee-api`**        | Go Redis client, Scylla driver |
| **`attendance-api`**      | Flask, psycopg2, Redis         |
| **`salary-api`**          | Spring Boot, JPA, MySQL/ES     |
| **`notification-worker`** | Redis Queue, smtplib           |
| **frontend**      | React, Axios, Traefik       |


---

## 6. Important Ports

| **Port** | **Service**               | **Description**         |
| -------- | ------------------------- | ----------------------- |
| 80     | Frontend/Traefik          | Main entry point        |
| 8080     | **`employee-api`**        | Employee service        |
| 8082     | **`salary-api`**          | Salary calculation      |
| 8081     | **`attendance-api`**      | Attendance management   |
| 9200    | **`Elasticsearch`** |  |Elasticsearch
| 6379     | Redis                     | Caching and queueing    |
| 5432     | PostgreSQL                | Attendance DB           |
| 9042     | ScyllaDB                  | Employee DB             |

---

## 7. Setup Instructions

| **Service**               | **Setup Guide**                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **`employee-api`**        | [View Setup](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/SCRUM-68-Ashutosh/OT-Microservices/Applications/Employee-API/Introduction/README.md)      |
| **`attendance-api`**      | [View Setup](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/scrum-7-aryan-mishra/OT-Microservices/Applications/Attendance-Api/Introduction/README.md) |
| **`salary-api`**          | [View Setup](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/scrum-70-abhishek-saini/0T-Microservices/Applications/Salary-Api/Introduction/README.md)  |
| **`notification-worker`** | [View Setup](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/scrum-63-anuj/OT-Microservices/Applications/Notification-API/Introduction/README.md)      |
| **`Frontend`** | [View Setup](https://github.com/Snaatak-Cloudops-Crew/documentation/tree/SCRUM-72-divya-mishra/OT-Microservices/Applications/Frontend-api/Introduction#readme)      |


---

## 8. Data Flow

| **Step** | **Component**             | **Action**                            |
| -------- | ------------------------- | ------------------------------------- |
| 1        | User (Frontend)           | Logs in / views dashboard             |
| 2        | **`employee-api`**        | Fetches user profile                  |
| 3        | **`attendance-api`**      | Records check-in/check-out            |
| 4        | **`salary-api`**          | Fetches attendance and calculates pay |
| 5        | **`notification-worker`** | Queues and sends salary notification  |

---

## 9. Troubleshooting

| **Issue**              | **Solution**                                              |
| ---------------------- | --------------------------------------------------------- |
| Redis not connecting   | Ensure Redis is running and accessible on port 6379       |
| DB connection fails    | Validate `.env` credentials and check firewall            |
| API not responding     | Ensure all services are running and healthy               |
| SMTP errors            | Check email credentials, SMTP port, and service status    |
| CORS / frontend issues | Validate proxy setup via Traefik and update CORS policies |

---

## 10. Conclusion

This full-stack HR system enables robust attendance tracking, salary computation, and employee management through modular microservices. Its scalable design allows independent development and deployment of services while maintaining performance and observability. Redis and databases serve as the backbone for service communication and data persistence.

---

## 11. Contact Information

| **Name** | **Email**                                                                     |
| -------- | ----------------------------------------------------------------------------- |
| Sonal    | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## 12. References

| **Technology** | **Official Documentation**                                     |
| -------------- | -------------------------------------------------------------- |
| employee-api        | [https://github.com/OT-MICROSERVICES/employee-api](https://github.com/OT-MICROSERVICES/employee-api)               |
| attendance-api      | [https://github.com/OT-MICROSERVICES/attendance-api](https://github.com/OT-MICROSERVICES/attendance-api)           |
| salary-api          | [https://github.com/OT-MICROSERVICES/salary-api](https://github.com/OT-MICROSERVICES/salary-api)                   |
| notification-worker | [https://github.com/OT-MICROSERVICES/notification-worker](https://github.com/OT-MICROSERVICES/notification-worker) |
| frontend            | [https://github.com/OT-MICROSERVICES/frontend](https://github.com/Snaatak-Cloudops-Crew/documentation/tree/SCRUM-72-divya-mishra/OT-Microservices/Applications/Frontend-api/Introduction#readme)                       |


---


