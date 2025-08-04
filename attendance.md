



# Attendance API – POC
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/77019615-6703-4dda-b369-ae1a18538506" />
---

## Author Information

| Created by | Created on | Version | Last Updated On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------- | ---------- | ------- | --------------- | ------------ | ----------- | ----------- | ----------- |
| Sonal      | 29-07-2025 | V 1.0   | 29-07-2025      | Anjali     |             |             |             |

---

## Table of Contents

* [Introduction](#introduction)
* [Purpose](#purpose)
* [Prerequisites](#prerequisites)
* [Architecture / Design](#architecture--design)
* [API Setup and Execution](#api-setup-and-execution)
* [Success Criteria](#success-criteria)
* [Result & Validation](#result--validation)
* [Troubleshooting Steps](#troubleshooting-steps)
* [Contact Information](#contact-information)
* [Conclusion](#conclusion)
* [References](#references)

---

## Introduction

The Attendance API is a Python 3.11-based microservice that provides a RESTful interface to manage employee attendance records. It leverages PostgreSQL and Redis as backend services and utilizes Gunicorn as its production-ready WSGI HTTP server. This POC demonstrates its deployment without Docker on an Ubuntu-based environment and validates endpoint functionality.

---

## Purpose

This document outlines the process of deploying and validating the functionality of the **Attendance API** microservice, available at [https://github.com/OT-MICROSERVICES/attendance-api](https://github.com/OT-MICROSERVICES/attendance-api). It includes setup steps, dependency installation, DB configuration, and successful execution of the application.

---

## Prerequisites

- ### Software Dependencies

| Dependency | Version / Info   |
| ---------- | ---------------- |
| Python     | v3.11+           |
| PostgreSQL | v14+             |
| Redis      | Latest stable    |
| Poetry     | Latest           |
| Gunicorn   | Latest           |
| Liquibase  | v4.27+           |
| Git        | Latest available |

- ### System Requirements

| Component        | Requirement       |
| ---------------- | ----------------- |
| Operating System | Ubuntu 22.04 LTS  |
| User Access      | Sudo privileges   |
| RAM              | Minimum **4 GB**  |
| CPU              | 2 vCPUs           |
| Disk             | 10 GB+ free space |

- ### Ports

| Port | Service        | Purpose                 |
| ---- | -------------- | ----------------------- |
| 8081 | Attendance API | REST API and Swagger UI |
| 5432 | PostgreSQL     | Relational database     |
| 6379 | Redis          | In-memory cache service |

---

## Architecture / Design

### High-Level Architecture

<img width="1073" height="465" alt="Screenshot 2025-08-04 081316" src="https://github.com/user-attachments/assets/5c452d29-0a9c-4183-9eb6-64c98c44a511" />


* **API** written in **Python 3.11+** using Flask.
* **PostgreSQL** as the relational data store.
* **Redis** for caching and background processing.
* **Liquibase** for database schema migration.
* **Gunicorn** as the production-ready WSGI server.

  
---

## API Setup and Execution



### Installing Dependencies for Attendance API

| **Tool**         | **Installation Steps**                                                                                                                                                                                |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Python 3.11+** | Follow this [link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Softwares/Python/Installation/README.md) to install and configure Python 3.11+                                    |
| **Redis**        | Follow this [link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/scrum-73-aryan-mishra/OT-Microservices/Softwares/Redis/POC/README.md) to install and configure Redis                   |
| **PostgreSQL**   | Follow this [link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/SCRUM-75-deepak/Softwares/Postgresql/POC/README.md) to install and configure PostgreSQL                                |
| **Liquibase**    | Follow this [link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Others/Liquibase/Installation/README.md) to install and configure Liquibase for DB migrations                     |
| **Poetry**       | Follow this [link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Others/Poetry/Installation/README.md) to install Poetry for dependency and environment management                 |
| **Gunicorn**     | Follow this [link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Others/Gunicorn/Installation/README.md) to install and configure Gunicorn for production WSGI application hosting |





## Configuring Steps

---

### 1. Clone the Repository

```bash
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
cd attendance-api/
```


---

### 2. Install Python 3.12

> Ensure Python 3.12 is installed. If not, install it manually by given [Link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Softwares/Python/Installation/README.md)

```bash
python3 --version
```


---

### 3. Set Up Python Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

---

### 4. Install Poetry

> Ensure Poetry is installed. If not, install it manually by given [Link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Others/Poetry/Installation/README.md)

```bash

poetry --version
```

---

### 5. Install Redis

> Ensure Redis is installed. If not, install it manually by given [Link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/scrum-73-aryan-mishra/OT-Microservices/Softwares/Redis/POC/README.md)

Verify Redis:

```bash
redis-server --version
sudo systemctl status redis-server
```


---

### 6. Install PostgreSQL

> Ensure PostgreSQL is installed. If not, install it manually by given [Link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/SCRUM-75-deepak/Softwares/Postgresql/POC/README.md)

Verify PostgreSQL:

```bash
psql --version
sudo systemctl status postgresql
```


Create DB and user:

```bash
sudo -i -u postgres
psql
ALTER USER postgres WITH PASSWORD 'password';
CREATE DATABASE attendance_db;
\q
exit
```

---

### 7. Install Liquibase

> Ensure Liquibase is installed. If not, install it manually by given [Link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Others/Liquibase/Installation/README.md)

```bash
sudo apt install -y openjdk-17-jre
java -version

cd ~
curl -LO https://github.com/liquibase/liquibase/releases/download/v4.27.0/liquibase-4.27.0.tar.gz
tar -xvzf liquibase-4.27.0.tar.gz
mv liquibase-4.27.0 liquibase
```

---

### 8. Configure the Application

Edit DB connection in:

```bash
nano config/config.yaml
```


Paste the following config:

```yaml
postgres:
  database: attendance_db
  host: localhost
  port: 5432
  user: postgres
  password: password

redis:
  host: localhost
  port: 6379
  password: ""
```

---

### 9. Configure Liquibase Properties

```bash
cd ~/attendance-api
nano liquibase.properties
```

Paste:

```
url=jdbc:postgresql://localhost:5432/attendance_db
driver=org.postgresql.Driver
username=postgres
password=password
changeLogFile=migration/db.changelog-master.xml
```

---

### 10. Fix `pyproject.toml` for Poetry

> Update the `pyproject.toml` file as below to avoid poetry errors.

```bash
nano pyproject.toml
```

Replace:

```toml
packages = [{ include = "attendance_api" }]
```

With:

```toml
package-mode = false
```

And replace:

```toml
psycopg2 = "^2.9.6"
```

With:

```toml
psycopg2-binary = "^2.9.6"
```

---

### 11. Install System Build Dependencies

```bash
sudo apt install -y libpq-dev python3-dev build-essential
sudo ln -s $(which python3) /usr/bin/python
```

---

### 12. Install Python Dependencies via Poetry

```bash
poetry lock
poetry install
```

If PostgreSQL causes errors:

```bash
sudo apt-get install --reinstall -y libpq-dev
which pg_config
poetry lock
poetry install
```

---

### 13. Run the Attendance API

> Ensure Gunicorn is installed. If not, install it manually by given [Link](https://github.com/Snaatak-Cloudops-Crew/documentation/blob/main/Others/Gunicorn/Installation/README.md)

```bash
poetry add gunicorn
poetry run gunicorn app:app -b 0.0.0.0:8080 --log-config log.conf
```


---

### 14. Verify via Swagger UI

Open in browser:

```
http://<your-public-ip>:8080/apidocs
```


You should see the interactive API documentation and be able to test endpoints:

| **Endpoint**                     | **Method** | **Description**                                |
| -------------------------------- | ---------- | ---------------------------------------------- |
| /metrics                         | GET        | Prometheus metrics for monitoring              |
| /api/v1/attendance/health        | GET        | Basic health check                             |
| /api/v1/attendance/health/detail | GET        | Full dependency health check (Postgres, Redis) |
| /api/v1/attendance/create        | POST       | Creates an attendance record                   |
| /api/v1/attendance/search        | GET        | Search attendance records via query parameters |
| /api/v1/attendance/search/all    | GET        | Fetch all attendance records                   |
| /apidocs                         | GET        | Swagger UI for the Attendance API              |



---

## Success Criteria

| Criterion              | Expected Outcome                     |
| ---------------------- | ------------------------------------ |
| API Build & Execution  | Gunicorn server starts without error |
| Swagger UI Access      | `:8080/apidocs` loads correctly      |
| PostgreSQL Integration | DB connection works as expected      |
| Redis Connection       | `redis-cli ping` returns `PONG`      |
| Liquibase Migration    | Runs successfully and creates tables |

---

## Result & Validation

| Test Case                         | Status  |
| --------------------------------- | ------- |
| Swagger UI loaded                 | Success |
| PostgreSQL connection established | Success |
| Redis service running             | Success |
| Gunicorn serving on port 8080     | Success |
| Liquibase migration completed     | Success |

---

## Troubleshooting Steps

| Issue                             | Cause                                   | Solution                                          |
| --------------------------------- | --------------------------------------- | ------------------------------------------------- |
| `500 Internal Server Error`       | DB or Redis not running, table missing  | Ensure services are running and DB is initialized |
| `psycopg2.errors.UndefinedTable`  | Table `records` missing                 | Create manually or rerun Liquibase                |
| Swagger UI loads but no endpoints | Improper Flask setup or import          | Check app structure and Flask config              |
| `curl` to health check fails      | Gunicorn not running or port blocked    | Restart API and check security group              |
| Redis ping fails                  | Redis not started or wrong IP in config | Start Redis and verify config.yaml                |

---

## Contact Information

| Name  | Email                                                                         |
| ----- | ----------------------------------------------------------------------------- |
| Sonal | [sonal.roha.snaatak@mygurukulam.co](mailto:sonal.roha.snaatak@mygurukulam.co) |

---

## Conclusion

This Proof of Concept demonstrates successful deployment of the **Attendance API** in a Linux environment without Docker. All dependencies are configured correctly and endpoints function as expected. The system is stable and ready for further enhancements, monitoring, or containerization.

---

## References

| Reference                  | Link                                                       |
| -------------------------- | ---------------------------------------------------------- |
| Attendance API GitHub Repo | [Link](https://github.com/OT-MICROSERVICES/attendance-api) |
| PostgreSQL Documentation   | [Link](https://www.postgresql.org/docs/)                   |
| Redis Documentation        | [Link](https://redis.io/docs/)                             |
| Poetry                     | [Link](https://python-poetry.org/docs/)                    |
| Liquibase                  | [Link](https://www.liquibase.org/docs/latest/home.html)    |

---
