## Project Overview

In this project, you will build a workflow whose behavior is controlled entirely by configuration data instead of hardcoded logic.

Most beginners build workflows where routing decisions are embedded directly inside IF nodes, Switch nodes, and expressions. This works initially, but becomes difficult to maintain as business rules change.

The goal of this project is to separate business configuration from workflow logic. Non-technical users should be able to change how the system behaves by editing a spreadsheet rather than modifying the workflow itself.

This project introduces an important software engineering principle:

**Configuration over Hardcoding**

Key concepts include:

- Dynamic Routing
- Configuration Management
- Workflow Flexibility
- Runtime Decision Making
- Business Rule Engines
- Maintainable Automations
- Client-Friendly Systems

This pattern appears frequently in enterprise automation projects because business rules change much faster than technical implementations.

---

# Client Scenario

## The Client

Omar runs a customer support outsourcing company.

His company handles requests for multiple clients.

Different request types must be routed to different teams:

|Request Type|Assigned Team|
|---|---|
|Technical Support|Technical Team|
|Billing Question|Finance Team|
|Refund Request|Refund Team|
|Sales Inquiry|Sales Team|
|Complaint|Customer Success Team|

Today, every routing rule is hardcoded inside workflows.

Whenever a client wants to change a rule:

- A developer must edit the workflow.
- The workflow must be retested.
- Mistakes occasionally occur.

Omar wants managers to control routing behavior themselves without touching N8N.

---

# Business Goal

When a support request arrives:

1. Read the request type.
2. Load routing rules from a configuration sheet.
3. Determine the destination dynamically.
4. Send notifications to the correct team.
5. Allow future changes without modifying the workflow.

The goal is to make routing configurable and maintainable.

---

# Technical Requirements From The Client

## Incoming Requests

Requests arrive through:

```text
Webhook Trigger
```

Example payload:

```json
{
  "ticket_id": "T-1023",
  "customer_name": "Sarah Ahmed",
  "request_type": "Refund Request",
  "message": "I would like a refund."
}
```

---

## Configuration Sheet

Store routing rules in:

```text
Google Sheets
```

Example:

|Request Type|Destination Team|Notification Channel|
|---|---|---|
|Technical Support|Tech Team|Slack|
|Billing Question|Finance Team|Email|
|Refund Request|Refund Team|Slack|
|Sales Inquiry|Sales Team|Email|
|Complaint|Customer Success|Slack|

Managers should be able to update this sheet without touching the workflow.

---

## Dynamic Routing Logic

The workflow must:

1. Receive request.
2. Load configuration.
3. Find matching rule.
4. Determine routing destination.
5. Execute correct action.

No request types should be hardcoded inside IF or Switch nodes.

---

## Team Notification

Depending on configuration:

### Slack Route

Send notification to:

```text
Configured Slack Channel
```

Example:

```text
New Refund Request received.
Ticket ID: T-1023
```

---

### Email Route

Send notification to:

```text
Configured Team Email
```

---

## Unknown Request Handling

If no matching rule exists:

Route to:

```text
Fallback Support Queue
```

Send alert:

```text
Unconfigured Request Type Detected
```

---

## Configuration Cache

The client receives thousands of requests daily.

The workflow should not read Google Sheets on every execution.

Implement:

```text
Configuration Caching
```

Possible approaches:

- Variables
- Redis
- Data Store
- Scheduled Config Refresh Workflow

---

## Audit Logging

Store routing history:

|Field|Description|
|---|---|
|Ticket ID|Request identifier|
|Request Type|Incoming category|
|Destination|Routed team|
|Timestamp|Routing time|
|Rule Version|Configuration used|

Store logs in:

```text
Google Sheets
```

---

## Change Tracking

The client wants visibility into configuration changes.

Track:

- Who changed a rule.
- What changed.
- When it changed.

Optional storage:

```text
Google Sheets
```

or

```text
Airtable
```

---

## Failure Handling

If configuration cannot be loaded:

1. Stop routing.
2. Send alert.
3. Store failed request.

If destination notification fails:

1. Retry.
2. Escalate if retry fails.

---

## Tools Required

Core Nodes:

- Webhook Trigger
- Google Sheets
- IF Node
- Switch Node
- Slack
- Gmail

Optional:

- Redis
- Airtable
- N8N Data Store

---

# What The Learner Will Practice

By completing this project, you will learn:

### Configuration-Driven Design

Separating business rules from workflow logic.

### Dynamic Routing

Making runtime decisions using external data.

### Workflow Flexibility

Building systems that adapt without modification.

### Caching

Reducing unnecessary external reads.

### Audit Logging

Tracking workflow decisions for troubleshooting.

### Enterprise Architecture

Creating systems that scale operationally.

### Client-Friendly Automation

Allowing non-technical users to control behavior.

---

# Success Criteria

The project is complete when:

- Requests route successfully.
- Rules come from configuration.
- No routing logic is hardcoded.
- Managers can change behavior through the sheet.
- Unknown requests are handled safely.
- Logs are recorded.
- Configuration caching works.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Lead Assignment Engine

Route incoming leads to different sales representatives based on country, industry, or company size.

---

## Scenario 2 — Multi-Store Order Router

Route orders to different fulfillment centers based on product type or location.

---

## Scenario 3 — HR Ticket Routing System

Assign employee requests to payroll, recruitment, IT, or HR teams.

---

## Scenario 4 — Multi-Language Customer Support

Route tickets to support agents based on customer language.

---

## Scenario 5 — Marketing Campaign Router

Send leads into different marketing funnels based on campaign source.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Rule priorities.
- Conditional routing logic.
- Multi-step routing.
- Approval-based routing.
- Rule expiration dates.
- Environment-specific configurations.
- Self-service admin dashboard.
- AI-assisted routing recommendations.
- Multi-tenant configurations.
- Versioned configuration management.
- Real-time config updates.
- Advanced rule engine support.
- Dynamic workflow selection.
- Conflict detection.
- Full business rules management system.

---

# Production Insight

This project introduces a pattern commonly used in enterprise software:

**Request → Load Configuration → Evaluate Rules → Route → Log**

You will encounter this architecture in:

- Customer support platforms
- CRM systems
- Marketing automation tools
- ERP systems
- Workflow engines
- SaaS applications
- Enterprise integration platforms

One of the most important lessons from this project is that business rules change constantly. Every hardcoded rule becomes future maintenance work. By moving configuration outside the workflow and into a system that business users can manage themselves, you create automations that are easier to maintain, easier to scale, and significantly more valuable to clients. Many enterprise systems are built around this exact principle: the workflow remains stable while the business rules evolve independently.