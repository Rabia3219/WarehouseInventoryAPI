# Project Requirements Document
## Warehouse Inventory & Logistics Management System

---

## 1. Introduction

### Brief Project Description
The Warehouse Inventory & Logistics Management System is a backend REST API developed using Java and Spring Boot. The application provides digital tracking of stock items, warehouse bin allocations, automated background scheduling routines, and secure data persistence via a relational database to streamline modern supply chain management.

### Problem Statement
Traditional warehouse operations often suffer from human error, delayed tracking of incoming shipments, and manual, reactive monitoring of stock depletion. Without automated background processing, inventory discrepancies cause delayed fulfillment, unexpected stockouts, and fragmented communication between warehouse personnel and corporate stakeholders. This project resolves these issues by supplying an automated, reliable backend system capable of managing inventory data in real-time.

### Identify Stakeholders
*   **Warehouse Managers / Inventory Control Personnel:** Primary technical users interacting with the API endpoints to log items, audit stock quantities, and trace item locations.
*   **Operations Staff / Stakeholders:** Secondary recipients who rely on automated reporting logs, metrics, and external notification loops to manage supply chain actions.
*   **Academic Instructor / Evaluator:** The final stakeholder auditing the software's functional correctness, architecture compliance, and engineering documentation standards.

---

## 2. Requirements Gathering

### How Requirements Were Identified
The requirements for this system were identified using an engineering framework mapping technical course constraints to real-world logistics challenges:
1.  **Core Feature Mapping:** The instructor-mandated framework requiring all four core HTTP methods (GET, POST, PUT, DELETE) directly established the need for standard inventory management endpoints (View, Add, Edit, Delete).
2.  **Automation Analysis:** Background task requirements were evaluated based on standard warehouse triggers, identifying automated inventory audits (low stock checking) and automated reporting (external status broadcasts) as critical system automations.
3.  **Prototyping & Database Modeling:** Iterative domain modeling sessions were conducted to isolate standard database relationships, resulting in a system design capable of persisting structural schemas across runtime errors.

---

## 3. Use Cases 

### Use Case 1: Create and Log a New Product Variant
*   **Goal:** Add an incoming product line securely to the warehouse inventory database.
*   **Scope:** Backend REST API / Database Entity Layer.
*   **Preconditions:** The user must provide a uniquely identifiable SKU code and standard item details via an authenticated client payload.
*   **Success Conditions:** A new database entry is committed with a unique identifier, and the application responds with a standard HTTP 201 Created status.
*   **Failure Conditions:** The request returns an HTTP 400 Bad Request or HTTP 409 Conflict status; no database mutation occurs.
*   **Actors:** Warehouse Inventory Control Personnel.
*   **Trigger:** An API `POST` request is received at the `/api/inventory` endpoint containing the product body payload.
*   **Main Scenario:**
    1. Actor sends a POST request with structural product attributes (SKU, Name, Current Quantity, Low-Stock Threshold).
    2. System intercepts the incoming request payload and executes formatting validation checks.
    3. System queries the relational database to ensure the provided SKU does not already exist.
    4. System builds a persistent inventory entry and commits it to the database table.
    5. System returns a success message object alongside the saved resource data.
*   **Extensions / Variations:**
    *   *3a. SKU Collision:* If the SKU code matches an existing entry, the system rejects the transaction and throws a custom exception handler.
    *   *2a. Missing Data:* If mandatory payload attributes (e.g., negative stock quantity fields) fail backend entity validations, processing ceases instantly.
*   **Related Info:** Intersects with database transaction logging rules.
*   **Open Issues:** None identified.

### Use Case 2: Automated Low-Stock Alert Sweep
*   **Goal:** Automatically monitor data tables to identify, tag, and trigger alert responses for critically depleted inventory variants.
*   **Scope:** Automated Spring Boot Internal Task Scheduler.
*   **Preconditions:** The application runtime must be continuously operational, and active data records must occupy the inventory tables.
*   **Success Conditions:** Decongested database checks finish completely, accurate logs identify low-stock records, and external warning actions fire successfully.
*   **Failure Conditions:** The scheduler drops execution tasks, database connection pools time out, or external alerting mechanisms fail to accept payload warnings.
*   **Actors:** Automated System Background Engine (System Actor).
*   **Trigger:** An internal cron timer or specific scheduling constraint ticks over to trigger automated execution routines.
*   **Main Scenario:**
    1. The internal `@Scheduled` framework wakes up the automated service engine.
    2. System executes an inner-join database query pulling items where `Current Quantity <= Low-Stock Threshold`.
    3. System loops through the dirty collection records, setting active internal warning flags to alert managers.
    4. System initiates an integrated broadcast action simulating an external operational notice channel update.
    5. System saves the updated states and safely returns back to an idle execution posture.
*   **Extensions / Variations:**
    *   *2a. Empty Set:* If zero inventory records drop beneath their respective threshold baselines, the task logs a clean baseline confirmation and finishes quietly.
*   **Related Info:** Maps directly to assignment background task regulations.
*   **Open Issues:** Defining strict notification rate-limiting thresholds to avoid system logging spam.

---

## 4. Validation 

### How Requirements Will Be Validated
To verify the system fully adheres to all established technical and operational specifications, the team will implement a multi-tiered validation approach:
1.  **Endpoint Testing (Postman):** Every core HTTP method endpoint (`GET`, `POST`, `PUT`, `DELETE`) will be systematically hit using parameterized Postman collection tests to validate that response payloads, success codes, and error exceptions behave as intended.
2.  **Database Inspection:** Manual database querying will be conducted post-execution to confirm that entity writes, schema relations, and field updates are correctly written to disk and persist over server resets.
3.  **Task Automation Verification:** The background execution logs will be scrutinized over extended run windows to check that scheduled sweeping triggers drop into action at the exact specified runtime intervals.
4.  **Live Environment Mocking:** Sandbox tracking tools will catch external simulated broadcasts to verify that automated payloads are structured correctly for external deployment.
