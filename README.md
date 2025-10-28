# Web Application Penetration Testing Lab (Kali + DVWA)
## Overview
This project provides an isolated lab environment for practicing fundamental **Web Application Penetration Testing** skills. It specifically targets 2 vulnerabilities from the **OWASP Top 10**: **SQL Injection (SQLi)** and **Cross-Site Scripting (XSS)**.

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
1. **Access DVWA**: Open your web browser and navigate to: `http://localhost:8080`.
2. **Login**: Use the default credentials: `admin`/`password`.
3. **Initialise**: Click the **"Create/Reset Database"** button.
4. **Set Security**: Navigate to **"DVWA Security"** and set the level to `Low`.
### Access the Kali Terminal
Attach the Kali container to start running your penetration testing tools.
```
docker exec -it kali-attacker /bin/bash
```

---

## Lab Walkthrough

### Reconnaissance and Setup
1. **Find the Target Hostname**:
```
# Container name is 'dvwa-victim'
nmap -sn dvwa-victim
```
2. **Install SQLMap**:
```
apt update && apt install sqlmap -y
```
### SQL Injection (SQLi) - Automated Database Compromise
1. **Capture Cookies**: In the browser (while logged into DVWA), open **Developer Tools** (F12) and find the `PHPSESSID` cookie value under the **Application** or **Storage** tab and copy this value.
2. **Run SQLMap to Dump Credentials**:
```
# Replace <Your_Session_ID> with the copied value
sqlmap -u "http://dvwa-victim/vulnerabilities/sqli/" --data="id=1&Submit=Submit" --cookie="security=low; PHPSESSID=<Your_Session_ID>" --dbs
```
Success is confirmed when SQLMap displays a table listing the usernames and hashed passwords from the database.
### Cross-Site Scripting (XSS) - Stored Payload
1. **Navigate**: In the browser, go to the **"XSS (Stored)"** page.
2. **Payload**: Use the following script in the **"Message"** field to demonstrate cookie theft/display:
```
<script>alert(document.cookie);</script>
```
3. **Observation**: A JavaScript pop-up alert box should appear, displaying the current session cookies. This confirms the application is vulnerable to Stored XSS because it fails to sanitise user input.

---

## Conclusion
This lab successfully demonstrated the practical execution of two critical web application flaws: **SQL Injection (SQLi)** and **Cross-Site Scripting (XSS)**. By utilizing industry-standard tools like **SQLMap** within the isolated **Kali Linux** environment, this project provides hands-on experience exploiting vulnerabilities rooted in insecure data handling and improper input sanitization and reinforces the importance of viewing application security from the attacker's perspective.

**Disclaimer**: This lab was conducted in a controlled, isolated environment for educational purposes. Unauthorised access to any computer system is illegal and unethical.
