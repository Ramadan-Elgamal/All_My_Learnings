## Project Overview

In this project, you will use N8N to build a small REST API backend without writing a traditional server application.

Using Webhook nodes, Google Sheets as a database, and structured JSON responses, you will create API endpoints that allow external applications to create, read, update, and manage data.

This project demonstrates that automation platforms can do more than connect apps—they can also act as lightweight backend services.

You will learn:

- REST API fundamentals
- Webhook-based APIs
- CRUD operations
- JSON responses
- Request validation
- API design
- Data persistence using Google Sheets

This project is particularly valuable for developers because it bridges traditional backend concepts with workflow automation.

---

# Client Scenario

## The Client

Sarah owns a small fitness coaching business.

She wants to launch a simple mobile application where clients can:

- Register themselves
- View their profile
- Update personal information
- Track memberships

Hiring a backend developer to build a custom API is currently outside her budget.

She already uses Google Sheets to manage client information and wants a lightweight solution that can serve as a backend for her app.

Sarah needs an API that her mobile app can call to create and retrieve client data.

---

# Business Goal

Build a REST-style API using N8N that allows external applications to:

1. Create records.
2. Read records.
3. Update records.
4. Return structured JSON responses.
5. Store all data in Google Sheets.

The goal is to provide backend functionality without maintaining a traditional server.

---

# Technical Requirements From The Client

## Data Storage

Use:

```text
Google Sheets
```

Database columns:

|ID|Name|Email|Membership Type|Created At|
|---|---|---|---|---|

---

# API Endpoints

## Create Client

### Endpoint

```http
POST /clients
```

### Request Body

```json
{
  "name": "Ahmed Hassan",
  "email": "ahmed@example.com",
  "membership": "Premium"
}
```

### Expected Response

```json
{
  "success": true,
  "id": "CL-1001"
}
```

---

## Get Client

### Endpoint

```http
GET /clients?id=CL-1001
```

### Expected Response

```json
{
  "id": "CL-1001",
  "name": "Ahmed Hassan",
  "email": "ahmed@example.com",
  "membership": "Premium"
}
```

---

## Update Client

### Endpoint

```http
POST /clients/update
```

### Request Body

```json
{
  "id": "CL-1001",
  "membership": "VIP"
}
```

### Expected Response

```json
{
  "success": true
}
```

---

## Error Responses

Example:

```json
{
  "success": false,
  "message": "Client not found"
}
```

---

# Validation Rules

Before writing data:

### Required Fields

- Name
- Email

### Email Validation

Email must:

- Exist
- Follow a valid email format

### Duplicate Prevention

Do not allow two clients with the same email address.

---

# Security Requirements

Implement:

- Header Authentication
- API Key Verification

Example:

```http
X-API-Key: abc123
```

Reject requests without a valid API key.

---

# Response Requirements

All responses should:

- Return JSON
- Include success status
- Include meaningful error messages

---

# Failure Handling

If Google Sheets is unavailable:

- Return a structured error response
- Log the failure

If invalid data is submitted:

- Return validation errors

---

# Tools Required

- Webhook Node
- Google Sheets Node
- IF Node
- Set Node
- Respond to Webhook Node

Optional:

- Data Store
- Airtable
- Code Node

---

# What The Learner Will Practice

By completing this project, you will learn:

### REST API Design

Understanding how APIs expose functionality.

### CRUD Operations

Creating, reading, and updating records.

### JSON Data Structures

Sending and receiving structured data.

### Request Validation

Protecting systems from bad input.

### Authentication

Securing APIs using API keys.

### Webhook Development

Turning N8N workflows into backend services.

### Backend Thinking

Building systems that other applications consume.

---

# Success Criteria

The project is complete when:

- API endpoints are accessible.
- Data can be created successfully.
- Data can be retrieved successfully.
- Data can be updated successfully.
- Authentication works correctly.
- Validation rules are enforced.
- JSON responses are returned consistently.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Book Library API

Manage books.

Endpoints:

```http
POST /books
GET /books
POST /books/update
```

Store:

- Title
- Author
- Category
- ISBN

---

## Scenario 2 — Student Management API

Manage students.

Store:

- Student ID
- Name
- Grade
- Department

Endpoints for:

- Registration
- Lookup
- Updates

---

## Scenario 3 — Inventory API

Manage inventory items.

Store:

- SKU
- Product Name
- Quantity
- Price

Provide:

- Create
- Read
- Update endpoints

---

## Scenario 4 — Appointment Booking API

Manage appointments.

Store:

- Customer
- Date
- Service

Allow:

- Create bookings
- Retrieve bookings
- Cancel bookings

---

## Scenario 5 — Event Registration API

Allow event attendees to register.

Store:

- Name
- Email
- Ticket Type

Provide:

- Registration endpoint
- Attendee lookup endpoint

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Implement DELETE endpoints.
- Add pagination.
- Add filtering and searching.
- Add rate limiting.
- Generate API documentation automatically.
- Create reusable validation middleware workflows.
- Replace Google Sheets with Airtable.
- Replace Google Sheets with PostgreSQL.
- Add JWT authentication.
- Add role-based access control.
- Add request logging.
- Create API usage analytics.
- Build versioned endpoints (`/v1`, `/v2`).
- Add webhook callbacks.
- Create a full CRUD framework using reusable sub-workflows.

---

# Production Insight

This project introduces one of the most important software architecture patterns:

**Request → Validate → Process → Respond**

You will encounter this pattern in:

- REST APIs
- GraphQL servers
- SaaS platforms
- Mobile application backends
- Internal business systems
- Integration platforms
- Microservices

One of the biggest mindset shifts when learning N8N is realizing that workflows are not limited to automations that start on a schedule. They can also behave like backend services that receive requests from external systems and return structured responses, opening the door to building lightweight applications without managing traditional server infrastructure.