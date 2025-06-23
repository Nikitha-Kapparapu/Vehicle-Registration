# Reservation-Service Module Low-Level Documentation

This document provides a low-level overview of the Reservation-Service module, a microservice within the Parking Management System (PMS) responsible for managing parking slot reservations.

---

## 1. Project Overview

The **Reservation-Service** is a Spring Boot-based application that manages parking slot reservations. It offers RESTful APIs for creating, updating, retrieving, and cancelling reservations. The service interacts with a database to persist reservation data and follows a layered architecture to ensure scalability and maintainability.

### Features

- **Create Reservations**
    * Accepts reservation requests with slot and time data.
    * Validates input and checks for overlapping reservations.
    * Saves the reservation to the database.
- **Retrieve Reservations**
    * Fetch reservation(s) by reservation ID or user ID.
    * Supports querying all reservations for a specific user.
- **Update Reservations** 
    * Allows users to reschedule bookings with updated time slots and vehicle information.
- **Cancel Reservations**
    * Deletes an existing reservation.
    * Ensures slot availability updates accordingly.

---

## 2. Architecture

### 2.1 High-Level Architecture

The Registration-Service module is built using the Spring Boot framework and adheres to a layered architecture. It communicates with other services via REST APIs and utilizes H2 as its database for local development purposes.

### 2.2 Layered Architecture

<pre><code>```mermaid graph TD UI[User Interface] API[ReservationController (REST API)] Service[ReservationServiceImpl (Business Logic)] Repo[ReservationRepository (JPA Repository)] DB[(Reservations Table)]

UI --> API API --> Service Service --> Repo Repo --> DB

subgraph Integration AuthService[Auth-Service] UserService[User-Service] SlotService[Slot-Availability-Service] end

Service --> AuthService Service --> UserService Service --> SlotService

### 2.3 Technologies Used

- **Framework**: Spring Boot  
- **Database**: H2 / MySQL  
- **Language**: Java  
- **Build Tool**: Maven  

---

## 3. Database Design

### 3.1 Table: `reservations`

| Column Name      | Data Type | Constraints                     |
|------------------|-----------|----------------------------------|
| reservation_id   | bigint    | Primary Key, Auto Increment      |
| user_id          | bigint    | Not Null                         |
| slot_id          | bigint    | Not Null                         |
| vehicle_number   | varchar   | Not Null                         |
| start_time       | datetime  | Not Null                         |
| end_time         | datetime  | Not Null                         |
| status           | varchar   | Not Null                         |

---

## 4. API Endpoints

### 4.1 Reservation Management

| Endpoint                             | Method | Description                       | Request Body / Params       |
|--------------------------------------|--------|-----------------------------------|-----------------------------|
| `/api/reservations`                 | POST   | Create a new reservation          | ReservationRequest          |
| `/api/reservations/user/{userId}`  | GET    | Get all reservations for a user   | userId (Path Variable)      |
| `/api/reservations/{id}`           | GET    | Get reservation by ID             | id (Path Variable)          |
| `/api/reservations/{id}`           | PUT    | Update reservation details        | ReservationUpdateRequest    |
| `/api/reservations/{id}`           | DELETE | Cancel a reservation              | id (Path Variable)          |

---

## 5. Application Flow

1. **User Interaction** – via REST API requests.
2. **Controller Layer** – maps requests to service methods.
3. **Service Layer** – executes business logic.
4. **Repository Layer** – communicates with the database.
5. **Database** – stores and manages reservation records.

---

## 6. Error Handling

Spring Boot’s exception handling is used to provide appropriate HTTP responses.

| Error Code | Description                     |
|------------|---------------------------------|
| 400        |
