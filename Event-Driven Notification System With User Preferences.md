## Project Overview

In this project, you will build a notification system that delivers messages to users based on their individual preferences.

Most beginner notification workflows are hardcoded:

```text
New Order → Send Email
```

or

```text
New Ticket → Send Slack Message
```

This works initially, but becomes difficult to maintain as users have different preferences.

Some users prefer:

- Email
- Slack
- Microsoft Teams
- Telegram
- WhatsApp

Some users want notifications only during working hours.

Some want urgent alerts immediately but non-critical notifications batched into a daily summary.

The goal of this project is to build a flexible notification engine where delivery behavior is controlled by user preferences instead of workflow logic.

This introduces an important software architecture concept:

**Separate business logic from notification delivery logic.**

---

# Client Scenario

## The Client

A software company uses an internal ticketing system.

Whenever events happen, employees need to be notified.

Examples:

- New support ticket assigned
- Critical server outage
- New customer signup
- Payment failure
- Project deadline approaching

The company currently sends all notifications through email.

Employees are unhappy because:

- Developers prefer Slack.
- Managers prefer Email.
- Operations staff use Microsoft Teams.
- Some employees only want notifications during business hours.
- Others want instant alerts for critical incidents.

The company wants a centralized notification system that respects user preferences automatically.

---

# Business Goal

When an event occurs:

1. Determine who should be notified.
2. Read each user's preferences.
3. Deliver notifications using the correct channel.
4. Respect quiet hours.
5. Log all deliveries.
6. Allow administrators to change preferences without editing workflows.

---

# Technical Requirements From The Client

## Event Sources

The system should support events from:

### Support System

```text
New Ticket Assigned
```

---

### Monitoring System

```text
Server Down
```

---

### CRM

```text
New Lead Created
```

---

### Billing System

```text
Payment Failed
```

---

### Project Management Tool

```text
Task Overdue
```

---

## Event Payload

Example:

```json
{
  "event_type": "server_down",
  "severity": "critical",
  "message": "Production API unavailable",
  "timestamp": "2026-01-15T10:00:00Z"
}
```

---

## User Preferences Database

Store preferences in:

```text
Google Sheets
```

or

```text
Airtable
```

or

```text
Notion
```

Example:

|User|Email|Slack|Teams|Quiet Hours|
|---|---|---|---|---|
|Ahmed|Yes|No|No|10 PM - 7 AM|
|Sara|No|Yes|No|None|
|Omar|Yes|Yes|No|11 PM - 6 AM|
|Fatma|No|No|Yes|None|

---

## Notification Rules

### Example Event

```text
New Ticket Assigned
```

---

User A:

```text
Email Only
```

Action:

```text
Send Email
```

---

User B:

```text
Slack Only
```

Action:

```text
Send Slack Message
```

---

User C:

```text
Email + Slack
```

Action:

```text
Send Both
```

---

## Severity-Based Routing

### Critical Event

Example:

```text
Server Down
```

Always send immediately.

Ignore quiet hours.

---

### Normal Event

Example:

```text
Task Assigned
```

Respect quiet hours.

---

## Quiet Hours Logic

Example:

User preference:

```text
10 PM - 7 AM
```

Current time:

```text
11:30 PM
```

Action:

```text
Delay Notification
```

until quiet hours end.

Use:

```text
Wait Node
```

for delayed delivery.

---

## Channel Support

The system must support:

### Email

Using Gmail.

---

### Slack

Using Slack node.

---

### Microsoft Teams

Using Teams webhook.

---

### Telegram

Optional extension.

---

### WhatsApp

Optional extension.

---

## Notification Template System

Templates should be configurable.

Example:

### Ticket Assigned

```text
You have been assigned ticket #123.
```

---

### Server Down

```text
Critical Alert: Production API is unavailable.
```

Templates should be stored in:

```text
Google Sheets
```

or

```text
Database
```

not hardcoded in the workflow.

---

## Delivery Logging

Every notification should be logged.

Store:

|Field|Description|
|---|---|
|User|Recipient|
|Event|Event Type|
|Channel|Delivery Method|
|Status|Success / Failure|
|Timestamp|Delivery Time|

---

## Failure Handling

### Example

Slack API unavailable.

Action:

1. Retry delivery.
2. Log failure.
3. Notify administrator if retries fail.

---

## User Preference Updates

Managers should be able to update preferences without touching N8N.

Example:

Employee changes:

```text
Slack = Yes
```

to

```text
Slack = No
```

The next notification should automatically follow the new preference.

---

## Monitoring Dashboard

Track:

|Metric|Description|
|---|---|
|Notifications Sent|Total|
|Delivery Failures|Errors|
|Channel Usage|Per platform|
|Delayed Notifications|Quiet hour delays|
|Critical Alerts|High-priority events|

---

## Security

The client wants:

- Authorized access to preference data.
- Secure notification credentials.
- Audit trail of preference changes.

---

## Tools Required

Core Nodes:

- Webhook
- Google Sheets
- IF Node
- Switch Node
- Wait Node
- Gmail
- Slack

Optional:

- Microsoft Teams
- Telegram
- WhatsApp
- Airtable
- Notion

---

# What The Learner Will Practice

By completing this project, you will learn:

### Event-Driven Architecture

Responding to events as they occur.

### Dynamic Configuration

Driving workflow behavior from data.

### Notification Routing

Selecting channels dynamically.

### User Preference Management

Building customizable systems.

### Scheduling Logic

Implementing quiet hours.

### Delivery Tracking

Monitoring notification success.

### Enterprise Automation Patterns

Building scalable communication systems.

---

# Success Criteria

The project is complete when:

- Events trigger notifications.
- User preferences are loaded dynamically.
- Correct channels are selected.
- Quiet hours are respected.
- Critical alerts bypass delays.
- Deliveries are logged.
- Failures are handled.
- Administrators can modify behavior without editing workflows.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — E-Commerce Customer Notification Center

Notify customers about orders, shipments, and refunds using their preferred channels.

---

## Scenario 2 — School Parent Communication System

Send attendance alerts, exam reminders, and announcements based on parent preferences.

---

## Scenario 3 — Healthcare Appointment Notification Platform

Deliver appointment reminders through email, SMS, WhatsApp, or phone-call scheduling.

---

## Scenario 4 — Internal IT Alerting System

Route infrastructure alerts to different teams based on severity and on-call schedules.

---

## Scenario 5 — SaaS Product Notification Hub

Handle product updates, billing notifications, and account alerts according to user settings.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Daily digest notifications.
- Weekly summary emails.
- User-defined notification priorities.
- Escalation chains for critical incidents.
- On-call engineer schedules.
- Multi-language notification templates.
- AI-generated notification summaries.
- Read receipt tracking.
- Notification throttling.
- Push notification support.
- Preference management portal.
- A/B testing notification templates.
- Multi-tenant notification routing.
- Notification analytics dashboard.
- Enterprise notification platform architecture.

---

# Production Insight

This project teaches an architecture used in many large-scale systems:

**Event → Preference Engine → Routing → Delivery → Logging**

You will find similar designs in:

- Slack
- Microsoft Teams
- Jira
- ServiceNow
- Zendesk
- HubSpot
- Enterprise alerting platforms

A common beginner mistake is embedding notification decisions directly into workflows. Professional systems separate event generation from notification delivery. This allows administrators to change channels, schedules, and preferences without modifying automation logic. The result is a system that is far easier to maintain, scale, and customize as the organization grows.