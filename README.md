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

## 🐳 Lab Setup Guide

The entire lab environment is deployed using a single `docker-compose.yml` file.

