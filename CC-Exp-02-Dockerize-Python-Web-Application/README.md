# Docker Lab — Experiment 2
# Containerize and Run a Simple Python Web Application

---

## 1. Experiment Title

**Containerize and Run a Simple Python Web Application**

---

## 2. Objective

To learn how to create a simple Python web application, package it into a Docker image, run it as a Docker container, and access the application from a web browser.

---

## 3. Learning Outcomes

After completing this experiment, the student will be able to:

- Create a basic Python Flask web application.
- Create and understand a Dockerfile.
- Build a Docker image from application files.
- Create, start, stop, inspect, and remove a Docker container.
- Map a host port to a container port.
- Access a containerized application through a web browser.
- Understand the basic workflow of application containerization.

---

# 4. Requirements

The following hardware and software are required:

### Hardware Requirements

- Windows 10 or Windows 11 computer
- Intel Core i5 or equivalent processor
- 8 GB or 16 GB RAM
- At least 512 GB storage

### Software Requirements

- Docker Desktop installed and running
- Visual Studio Code installed
- Internet connection for downloading Docker base images and Python packages

> **Important:** Commands shown in code blocks are intended for **PowerShell** unless another location is explicitly mentioned. Application code and Dockerfile content are created using **Visual Studio Code**.

---

# 5. Pre-Lab Setup — Docker Desktop

Before starting Experiment 1, Docker Desktop should be installed and working.

## Docker Setup Flow

```text
Windows PC/Laptop
       |
       v
Is Docker installed?
    /       \
  YES        NO
   |          |
   v          v
docker      Open Browser
--version       |
   |            v
   |       Search Docker Desktop
   |            |
   |            v
   |       Download & Install
   |            |
   |            v
   |       Open Docker Desktop
   |            |
   \------------/
        |
        v
    PowerShell
        |
        v
docker --version
        |
        v
docker run hello-world
        |
        v
    Start the Lab
