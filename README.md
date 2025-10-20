# Web Application Penetration Testing (Kali + DVWA)
## Overview
This project provides an isolated, reproducible lab environment for practicing fundamental **Web Application Penetration Testing** skills. It specifically targets 2 vulnerabilities from the **OWASP Top 10**: **SQL Injection (SQLi)** and **Cross-Site Scripting (XSS)**.

The environment is made using Docker Compose, consisting of the **Kali Linux** attacker container and the **DVWA (Damn Vulnerable Web Application)** victim container.

---

## Prerequisites

To successfully run and complete this lab, the user must have the following software installed on the host machine:

* **Docker:** Required for running containerized applications.
* **Docker Compose:** Required for defining and managing the multi-container lab environment.
* **Web Browser:** Needed to interact with the DVWA web application at `http://localhost:8080`.

---

## Lab Setup Guide

The entire lab environment is deployed using a single `docker-compose.yml` file.

### Docker Config File
Download the `docker-compose.yml` file and add it to the directory that is going to be used to launch the environment.
### Start the Environment
Navigate to the project directory and execute the following command:
```
docker-compose up -d
```
### Initial Configuration
1. **Accecss DVWA**: Open your web browser and navigate to: `http://localhost:8080`.
2. **Login**: Use the default credentials: `admin`/`password`.
3. **Initialise**: Click the **"Create/Reset Database"** button.
4. **Set Security**: Navigate to **"DVWA Security"** and set the level to `Low` for the exercises.
### Access the Kali Terminal
Attach the Kali container to start running your penetration testing tools.
```
docker exec -it kali-attacker /bin/bash
```

---

## Lab Objectives and Walkthrough
