## Project Overview

In this project, you will build a single webhook endpoint that can serve multiple clients while dynamically routing requests based on the client making the request.

Many freelancers and agencies eventually face a scaling problem:

Instead of managing:

```text
Client A → Workflow A
Client B → Workflow B
Client C → Workflow C
Client D → Workflow D
```

they end up maintaining dozens of nearly identical workflows.

This quickly becomes difficult to maintain, expensive to update, and prone to mistakes.

The solution is a **multi-tenant architecture** where one workflow serves many clients and changes its behavior dynamically based on configuration.

The goal of this project is to build a webhook dispatcher that:

- Identifies the client.
- Loads the client's configuration.
- Routes the request appropriately.
- Processes the request using client-specific settings.
- Logs activity per client.

This project introduces one of the most important architectural concepts used in SaaS products and agency automation systems.

---

# Client Scenario

## The Client

Sara runs an automation agency.

She manages automations for:

- Real Estate Companies
- Medical Clinics
- Marketing Agencies
- E-Commerce Stores
- Educational Platforms

Every client submits leads through a webhook.

Currently, Sara has:

```text
25 separate workflows
```

doing nearly the same thing.

The only differences are:

- Which Slack channel receives notifications.
- Which email address gets alerts.
- Which CRM receives data.
- Which team handles the lead.

Maintaining all these workflows is becoming a nightmare.

She wants one centralized workflow capable of serving all clients.

---

# Business Goal

When a webhook request arrives:

1. Identify the client.
2. Verify the client is authorized.
3. Load the client's configuration.
4. Route the request.
5. Execute the correct actions.
6. Log activity for that client.

The goal is to support many customers without duplicating workflows.

---

# Technical Requirements From The Client

## Incoming Webhook

The workflow should expose a single endpoint:

```text
POST /lead-intake
```

Example request:

```json
{
  "client_id": "clinic_001",
  "lead_name": "Ahmed Hassan",
  "phone": "+201234567890"
}
```

---

Alternative identification:

```http
X-API-Key: abc123xyz
```

The workflow should support:

- Client ID
- API Key
- Custom Header

---

## Client Identification

Each request must be matched to a client.

Possible lookup source:

```text
Google Sheets
```

Example:

|Client|API Key|
|---|---|
|Clinic A|key_123|
|Agency B|key_456|
|Store C|key_789|

---

If no match is found:

Return:

```http
401 Unauthorized
```

---

## Client Configuration

After identification, load client-specific settings.

Example configuration:

|Setting|Value|
|---|---|
|CRM|HubSpot|
|Notification Channel|Slack|
|Slack Channel|#sales|
|Welcome Email|Enabled|
|Lead Owner|Team A|

Store configuration in:

```text
Google Sheets
```

or

```text
Airtable
```

or

```text
Database
```

---

## Dynamic Routing

The workflow should change behavior based on configuration.

### Example Client A

Requirements:

- Save lead to HubSpot
- Notify Slack
- Send welcome email

---

### Example Client B

Requirements:

- Save lead to Airtable
- Send WhatsApp notification
- No email

---

### Example Client C

Requirements:

- Save lead to Google Sheets only

---

The workflow should decide what to do at runtime.

---

## Lead Processing

Incoming leads should be validated.

Required fields:

- Name
- Phone
- Email (optional)

Invalid submissions should return:

```http
400 Bad Request
```

---

## Security Requirements

Every request must pass:

### API Key Validation

Verify the key belongs to the client.

---

### Request Logging

Track:

|Field|Description|
|---|---|
|Client ID|Request owner|
|Timestamp|Arrival time|
|Status|Success / Failure|
|Source IP|Optional|
|Processing Time|Duration|

Store logs in:

```text
Google Sheets
```

or

```text
Database
```

---

### Rate Limiting

Prevent abuse.

Example:

```text
100 requests per minute per client
```

Requests exceeding limits should return:

```http
429 Too Many Requests
```

---

## Response Handling

Successful response:

```json
{
  "success": true,
  "message": "Lead processed successfully"
}
```

---

Failed authentication:

```json
{
  "success": false,
  "message": "Invalid API Key"
}
```

---

## Client Metrics Dashboard

Track:

|Metric|Description|
|---|---|
|Total Requests|All incoming requests|
|Successful Requests|Completed|
|Failed Requests|Errors|
|Average Processing Time|Performance|
|Leads Processed|Business volume|

---

## Alerting

Notify administrators when:

### Unknown Client Attempts Access

Example:

```text
Unauthorized webhook request detected.
```

---

### Client Exceeds Rate Limits

Example:

```text
Client clinic_001 exceeded rate limits.
```

---

### Processing Failures

Example:

```text
Lead processing failed for client agency_002.
```

---

## Configuration Management

The client wants non-technical employees to manage routing.

They should be able to change:

- Notification channels
- Email recipients
- CRM destinations
- Feature flags

Without modifying the workflow.

Changes should be made through:

```text
Google Sheets
```

or

```text
Airtable
```

---

## Tools Required

Core Nodes:

- Webhook Trigger
- IF Node
- Switch Node
- HTTP Request
- Google Sheets
- Slack

Optional:

- HubSpot
- Airtable
- WhatsApp Cloud API
- PostgreSQL
- Redis

---

# What The Learner Will Practice

By completing this project, you will learn:

### Multi-Tenant Architecture

Serving multiple clients from a single workflow.

### Dynamic Configuration

Separating logic from configuration.

### Runtime Routing

Making workflow decisions dynamically.

### Authentication

Validating API keys securely.

### Rate Limiting

Protecting shared infrastructure.

### SaaS Design Patterns

Building systems that scale across customers.

### Maintainability

Reducing duplicated workflows.

---

# Success Criteria

The project is complete when:

- One webhook serves multiple clients.
- Clients are authenticated.
- Configuration loads dynamically.
- Routing changes based on client settings.
- Activity is logged.
- Rate limits are enforced.
- Metrics are collected.
- Non-technical staff can update configurations.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Multi-Tenant E-Commerce Order Processor

One webhook processes orders for multiple online stores.

---

## Scenario 2 — Multi-Tenant CRM Integration Platform

Different companies sync leads into different CRM systems.

---

## Scenario 3 — SaaS Form Submission Router

One form endpoint serves hundreds of customers.

---

## Scenario 4 — Multi-Client WhatsApp Notification Service

Clients send notifications through a shared infrastructure.

---

## Scenario 5 — Agency Automation Platform

A single automation system manages workflows for dozens of agency clients.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Per-client feature flags.
- Usage-based billing calculations.
- Client-specific workflows via sub-workflows.
- Custom response templates.
- API key rotation.
- Role-based administration.
- Tenant-specific dashboards.
- Client onboarding workflow.
- White-label support.
- Usage quotas.
- Redis-based rate limiting.
- Audit trails for configuration changes.
- Multi-region deployments.
- Self-service client portals.
- Enterprise SaaS architecture.

---

# Production Insight

This project introduces one of the most important software architecture patterns:

**Identify → Authenticate → Load Configuration → Route → Execute → Log**

You will encounter this architecture in:

- SaaS platforms
- CRM systems
- Marketing automation tools
- Agency platforms
- API gateways
- Integration platforms
- Enterprise software

The biggest lesson from this project is understanding the difference between building a workflow and building a platform. Beginners often create a new workflow for every customer. Experienced automation engineers build systems that adapt to different customers using configuration. This dramatically reduces maintenance, simplifies updates, and allows one workflow to scale to dozens or even hundreds of clients.