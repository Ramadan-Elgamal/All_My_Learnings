## Project Overview

In this project, you will build a complete approval system where a request is submitted through a form, reviewed by a manager, and then either approved or rejected.

The workflow will send approval links by email, wait for the manager's decision, update records, and notify the requester of the final outcome.

This project introduces one of the most important enterprise automation patterns:

- Human-in-the-loop workflows
- Approval systems
- Webhook-based actions
- State tracking
- Multi-step business processes
- Decision workflows

Approval workflows exist in nearly every organization, making this one of the most valuable projects for freelancers and automation consultants.

---

# Client Scenario

## The Client

Omar manages a growing software company.

Employees frequently submit requests such as:

- Vacation requests
- Equipment purchases
- Software license requests
- Training budget requests
- Remote work requests

Currently, employees send emails to managers, who often forget to respond.

Problems include:

- Requests getting lost in inboxes
- No visibility into request status
- No audit trail
- Delayed approvals

Omar wants a centralized approval workflow that automatically manages the entire process.

---

# Business Goal

When an employee submits a request:

1. Store the request.
2. Notify the manager.
3. Allow the manager to approve or reject with one click.
4. Update the request status.
5. Notify the employee.
6. Maintain an audit trail.

The goal is to eliminate manual tracking and provide a clear approval process.

---

# Technical Requirements From The Client

## Request Submission Form

Employees submit:

|Field|Type|
|---|---|
|Employee Name|Text|
|Employee Email|Email|
|Request Type|Dropdown|
|Reason|Long Text|
|Requested Amount (Optional)|Number|

---

## Data Storage

Store all requests in:

```text
Google Sheets
```

Columns:

|Request ID|Employee|Email|Type|Reason|Status|Submission Date|
|---|---|---|---|---|---|---|

Default status:

```text
Pending
```

---

## Manager Approval Email

When a request is submitted:

Send an email to:

```text
manager@company.com
```

The email must contain:

- Request details
- Approval link
- Rejection link

Example:

```text
Request: Training Budget

Employee: Ahmed

Approve:
https://workflow.com/approve?id=123

Reject:
https://workflow.com/reject?id=123
```

---

## Approval Logic

### Approve Link

When clicked:

- Update status to Approved
- Record approval timestamp
- Notify employee

---

### Reject Link

When clicked:

- Update status to Rejected
- Record rejection timestamp
- Notify employee

---

## Employee Notification

Example approval email:

```text
Your request has been approved.

Request Type:
Training Budget

Status:
Approved
```

Example rejection email:

```text
Your request has been rejected.

Request Type:
Training Budget

Status:
Rejected
```

---

## Audit Trail

Store:

- Submission date
- Decision date
- Final status
- Request ID

This allows management to track every request.

---

## Failure Handling

If Google Sheets is unavailable:

- Log the error
- Notify the administrator

If a request ID cannot be found:

- Return an error page
- Log the incident

---

## Tools Required

- N8N Form Trigger
- Google Sheets Node
- Gmail Node
- Webhook Node
- IF Node
- Set Node

Optional:

- Slack
- Airtable
- Notion

---

# What The Learner Will Practice

By completing this project, you will learn:

### Human-in-the-Loop Automation

Building workflows that require human decisions.

### Approval Systems

Designing approval and rejection flows.

### Webhook Actions

Using webhooks as action buttons.

### State Management

Tracking requests throughout their lifecycle.

### Data Persistence

Maintaining records across multiple workflow executions.

### Email Automation

Sending dynamic emails with actionable links.

### Enterprise Workflow Design

Building business processes that mirror real organizations.

---

# Success Criteria

The project is complete when:

- Employees can submit requests.
- Requests are stored successfully.
- Managers receive approval emails.
- Approval and rejection links work correctly.
- Status updates are saved.
- Employees receive final notifications.
- An audit trail exists for every request.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Vacation Request Approval

Employees submit vacation requests.

Approval Manager:

```text
HR Department
```

Workflow:

- Submit request
- HR approves or rejects
- Employee receives decision

---

## Scenario 2 — Purchase Approval System

Employees request purchases.

Examples:

- Laptops
- Monitors
- Office equipment

Approval based on amount:

- Under $500 → Team Lead
- Above $500 → Department Manager

---

## Scenario 3 — Marketing Campaign Approval

Marketing staff submit campaigns for review.

Approvers evaluate:

- Budget
- Target audience
- Content

Then approve or reject.

---

## Scenario 4 — Content Publishing Approval

Writers submit articles.

Editors:

- Approve
- Reject
- Request revisions

Before publication.

---

## Scenario 5 — Client Proposal Approval

Sales representatives submit proposals.

Management approves pricing before sending proposals to clients.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Add multiple approval levels.
- Require two approvals before completion.
- Create escalation reminders if no response is received.
- Automatically remind managers after 24 hours.
- Add comments when rejecting requests.
- Build an approval dashboard in Notion.
- Store approvals in Airtable instead of Google Sheets.
- Add Slack approval buttons.
- Generate PDF approval records.
- Add digital signatures.
- Route requests to different managers based on request type.
- Create approval analytics and reporting.
- Build a mobile-friendly approval page.
- Add role-based approval rules.
- Create a reusable approval engine that can be used across multiple workflows.

---

# Production Insight

This project introduces a core enterprise automation pattern:

**Submit → Review → Decide → Record → Notify**

You will find this pattern in:

- HR systems
- Procurement systems
- Expense approvals
- Compliance reviews
- Contract approvals
- Content publishing workflows
- Financial authorization systems

One of the biggest challenges in business automation is not automating machines—it is coordinating people. Approval workflows bridge that gap by combining automation with human decision-making, making them one of the most valuable and widely used workflow types in modern organizations.