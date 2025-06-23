# Reservation-Service Module Low-Level Documentation

This document provides a low-level overview of the `Reservation-Service` module, a microservice within the Parking Management System (PMS) responsible for managing parking slot reservations.

---

## 1. Project Overview

The `Reservation-Service` module is a critical component of the PMS, enabling users to create, update, view, and cancel parking slot reservations. It ensures data integrity, prevents double bookings, and works seamlessly with user and slot management services.

### Features

- **Create Reservations**
  - Accepts requests to book a parking slot for a specific time frame.
  - Validates availability before creating a record.
  - Prevents overlapping reservations for the same slot.

- **View Reservations**
  - Fetch reservations by user ID or reservation ID.
  - Supports filtering and sorting for better usability.

- **Update Reservations**
  - Allows modification of slot, time window, or vehicle number.
  - Validates updated data to avoid conflicts.

- **Cancel Reservations**
  - Allows users to cancel an existing reservation.
  - Updates reservation status accordingly by checking slot availability.

---

## 2. Architecture

### 2.1 High-Level Architecture

The `Reservation-Service` follows a **layered architecture** using **Spring Boot** and communicates with other PMS modules via REST APIs. The service relies on a relational database (e.g., MySQL or H2) to manage persistence.

### 2.2 Layered Architecture Diagram

```mermaid
graph TD
    A[API Gateway] --> B[Reservation Controller]
    B --> C[Reservation Service]
    C --> D[Reservation Repository]
    D --> E[Reservations Database]
    A -- Registers and Discovers --> F[Eureka Discovery Service]
    C -- Registers and Discovers --> F
