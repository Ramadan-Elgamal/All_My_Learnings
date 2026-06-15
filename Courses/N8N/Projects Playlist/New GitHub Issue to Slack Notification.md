## Project Overview

In this project, you will build an automation that monitors a GitHub repository and instantly notifies a Slack channel whenever a new issue is created.

The workflow acts as a bridge between development tools and team communication tools, ensuring that important issues are visible immediately without requiring team members to constantly check GitHub.

You will learn:

- GitHub webhooks
- Event-driven workflows
- Working with JSON payloads
- Slack notifications
- Message formatting
- Filtering logic
- Developer workflow automation

This is one of the most common automations used by software teams and DevOps departments.

---

# Client Scenario

## The Client

Sara runs a software development agency.

Her team maintains several products for different clients.

Currently, when users report bugs or submit feature requests on GitHub:

- Issues appear inside GitHub.
- Developers often don't notice them immediately.
- Important bugs sometimes sit for hours before someone sees them.
- Managers have no real-time visibility into new issues.

Sara wants every new issue to instantly appear in Slack so the team can react faster.

---

# Business Goal

Whenever a new GitHub issue is created:

1. Detect the issue automatically.
2. Extract important information.
3. Send a notification to Slack.
4. Include a direct link to the issue.
5. Help the team respond quickly.

The goal is to reduce response times and improve visibility across the development team.

---

# Technical Requirements From The Client

## GitHub Repository

Monitor:

```text
company-product-repository
```

Whenever a new issue is opened.

---

## Information To Include

The Slack notification should contain:

- Issue title
- Issue number
- Author
- Labels
- Creation date
- Direct GitHub URL

Example:

```text
🐞 New Issue Created

Title: Login page crashes on mobile
Issue #: #142
Author: john_doe
Labels: bug, high-priority

View Issue:
https://github.com/...
```

---

## Slack Destination

Send notifications to:

```text
#engineering-alerts
```

---

## Message Formatting

The message should:

- Use Slack Block Kit
- Highlight important information
- Make the issue link easy to access

---

## Business Rules

The client only wants notifications for:

- Bug reports
- High-priority issues

Do NOT notify for:

- Documentation issues
- Feature requests
- Enhancement requests

Use GitHub labels to determine which issues qualify.

---

## Failure Handling

If Slack is unavailable:

- Log the failure
- Notify the engineering manager via email

If GitHub sends an invalid payload:

- Ignore the event
- Record the failure

---

## Tools Required

- GitHub Trigger
- IF Node
- Slack Node

Optional:

- Set Node
- Gmail Node
- Google Sheets

---

# What The Learner Will Practice

By completing this project, you will learn:

### GitHub Webhooks

How GitHub pushes events to external systems.

### Event-Driven Automation

Building workflows that react instantly to changes.

### JSON Payload Analysis

Understanding and extracting data from webhook events.

### Filtering Logic

Using labels and conditions to control workflow behavior.

### Slack Notifications

Sending rich messages to team communication platforms.

### DevOps Automation

Automating engineering workflows.

### Real-Time Monitoring

Reducing delays between an event and a response.

---

# Success Criteria

The project is complete when:

- New GitHub issues trigger the workflow.
- Relevant issue information is extracted.
- Slack receives a formatted notification.
- Non-relevant issues are ignored.
- Team members can quickly access the issue link.
- No manual monitoring is required.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Pull Request Notification System

Notify developers when a new pull request is opened.

Include:

- PR title
- Author
- Branch name
- Review link

Post to:

```text
#code-review
```

---

## Scenario 2 — Customer Support Escalation Alerts

When a high-priority support ticket is created, notify the support team.

Include:

- Ticket ID
- Customer
- Priority
- Assigned agent

Post to:

```text
#support-alerts
```

---

## Scenario 3 — Security Vulnerability Monitoring

Notify the security team whenever a vulnerability issue is reported.

Include:

- Severity
- Affected component
- Reporter

Post to:

```text
#security-alerts
```

---

## Scenario 4 — Jira Ticket Notification System

Notify a Slack channel whenever a new Jira ticket is created.

Include:

- Ticket title
- Assignee
- Priority
- Link

Post to:

```text
#project-management
```

---

## Scenario 5 — Product Feedback Pipeline

When users submit product feedback, notify the product team.

Include:

- Feedback title
- Category
- Customer
- Submission link

Post to:

```text
#product-feedback
```

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Notify different Slack channels based on issue labels.
- Mention specific team members automatically.
- Detect critical issues and mark them as urgent.
- Create a Jira ticket automatically.
- Create a Notion page for each issue.
- Log all issues in Google Sheets.
- Send a daily issue summary report.
- Generate an AI summary of long issue descriptions.
- Detect duplicate issues using AI similarity checks.
- Add reaction buttons for quick triage.
- Notify different teams based on affected component.
- Create a dashboard showing issue trends.
- Track average response time per issue.
- Automatically assign issues to team members.
- Build a complete incident management workflow around critical issues.

---

# Production Insight

This project introduces a foundational engineering pattern:

**Event → Filter → Notify**

You will encounter this pattern everywhere in automation work:

- GitHub monitoring
- Security alerting
- Incident response
- Customer support escalations
- Order notifications
- Payment alerts
- System monitoring

Many operational workflows exist for one reason:

**making sure the right people know about important events as quickly as possible.**