# Assignment1_J2ee

# Assignment 1: Development of Enterprise Digital Evidence Chain of Custody System

## Student Details
**Name:** Linga Sai Srilaxmi  
**Student Number:** N01653528  

## Table of Contents
- [Overview](#overview)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Build & Deployment Instructions](#build--deployment-instructions)
- [JNDI Configuration in WildFly](#jndi-configuration-in-wildfly)



## Overview

This project implements a secure Java EE web application that simulates the backend system for a federal digital forensic agency. It allows secure registration, custody tracking, and status monitoring of digital evidence items using Spring Framework technologies, JPA, and Thymeleaf. The application is packaged and deployed as an EAR file to the WildFly server.

---

## Project Structure

```text
digital-evidence-app/          → Parent Maven module
├── digital-evidence-ejb/      → Business logic, Spring services, JPA entities
├── digital-evidence-web/      → Spring MVC controllers and Thymeleaf views
├── digital-evidence-ear/      → EAR module for deployment
````

Each module contains its own `pom.xml` and is managed through the main `digital-evidence-app/pom.xml`.

---

## Technologies Used

* Java 17
* Spring Framework 5.3+
* Spring Data JPA 2.7+
* Hibernate ORM
* Thymeleaf
* Maven (multi-module)
* Jakarta EE 10
* WildFly 30+
* JNDI-based datasource

---

## Build & Deployment Instructions

### 📦 Build the Project

1. **Clone the repository**

   ```bash
   git clone https://github.com//digital-evidence-app.git
   cd digital-evidence-app
   ```

2. **Build using Maven**
   Ensure Maven is installed. Run:

   ```bash
   mvn clean install
   ```

   This will build:

   * `digital-evidence-ejb.jar`
   * `digital-evidence-web.war`
   * `digital-evidence-ear.ear`

---

### 🚀 Deploy to WildFly

1. Start WildFly and access the admin console (`http://localhost:9990`).

2. Navigate to **Deployments → Add**.

3. Select the generated EAR file:
   `digital-evidence-ear/target/digital-evidence-ear.ear`

4. Click **Next → Save → Enable**.

5. Access the application at:
   [http://localhost:8080/digital-evidence-web](http://localhost:8080/digital-evidence-web)

---

## JNDI Configuration in WildFly

1. In `standalone.xml`, register a new datasource under `<datasources>`:

```xml
<datasource jndi-name="java:/jdbc/digitalEvidenceDS" pool-name="DigitalEvidencePool" enabled="true" use-java-context="true">
    <connection-url>jdbc:mysql://localhost:3306/digital_evidence</connection-url>
    <driver>mysql</driver>
    <security>
        <user-name>your_db_user</user-name>
        <password>your_db_password</password>
    </security>
</datasource>
```

2. Ensure `mysql-connector-java.jar` is deployed as a module or added in WildFly.

3. Use the above JNDI name in your `beans.xml` configuration for the `EntityManagerFactory`.

---

