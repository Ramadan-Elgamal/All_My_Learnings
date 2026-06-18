## Project Overview

In this project, you will build a monitoring system that watches all your N8N workflows, detects failures and performance issues, and provides a centralized health dashboard.

Most beginners only discover problems when:

- A client complains.
- An email was never sent.
- A webhook stopped working.
- An automation silently failed.

Professional automation systems require monitoring.

Just because a workflow is active does not mean it is healthy.

A workflow might:

- Fail repeatedly.
- Run slower than expected.
- Stop running entirely.
- Process fewer records than usual.
- Accumulate errors over time.

The goal of this project is to build a meta-workflow that monitors other workflows and alerts you before users notice problems.

This project introduces a critical production engineering concept:

**Observability**

You cannot manage what you cannot see.

---

# Client Scenario

## The Client

Mariam owns an automation agency.

Her team manages more than 60 active N8N workflows for clients.

Examples:

- Lead capture systems
- Customer onboarding workflows
- Reporting automations
- E-commerce integrations
- AI-powered assistants

The problem is that nobody knows when a workflow stops working until a client reports it.

Recent incidents include:

### Incident 1

A lead capture workflow failed for 3 days.

The client lost dozens of potential customers.

---

### Incident 2

A reporting workflow became extremely slow.

Reports that normally took:

```text
30 Seconds
```

started taking:

```text
15 Minutes
```

Nobody noticed.

---

### Incident 3

A scheduled workflow stopped running because credentials expired.

The team discovered the issue two weeks later.

---

Mariam wants a monitoring system that continuously checks workflow health and reports issues automatically.

---

# Business Goal

The monitoring system should:

1. Inspect workflow executions.
2. Detect failures.
3. Detect unusual delays.
4. Detect workflows that have stopped running.
5. Generate health reports.
6. Alert administrators.

The goal is to proactively identify problems before clients are affected.

---

# Technical Requirements From The Client

## Monitoring Scope

Monitor all active workflows.

For each workflow collect:

- Workflow Name
- Workflow ID
- Active Status
- Last Execution
- Last Successful Execution
- Last Failed Execution
- Average Runtime
- Total Executions

---

## Data Source

Use:

```text
N8N API
```

to retrieve workflow and execution information.

The monitoring workflow should query:

- Workflows
- Executions
- Execution statistics

---

## Failure Detection

Identify workflows that have:

### Consecutive Failures

Example:

```text
5 Failed Executions In A Row
```

Action:

```text
Create Alert
```

---

### High Failure Rate

Example:

```text
Failure Rate > 20%
```

during the last 24 hours.

Action:

```text
Create Alert
```

---

## Inactive Workflow Detection

Detect workflows that should run regularly but have stopped.

Example:

Expected:

```text
Every Hour
```

Actual:

```text
No Execution For 6 Hours
```

Action:

```text
Create Alert
```

---

## Performance Monitoring

Track execution duration.

Example:

Normal Runtime:

```text
30 Seconds
```

Current Runtime:

```text
4 Minutes
```

Action:

```text
Performance Warning
```

---

## Health Scoring

Calculate a health score.

Example:

|Score|Status|
|---|---|
|90–100|Healthy|
|70–89|Warning|
|Below 70|Critical|

Possible factors:

- Failure rate
- Runtime
- Missed schedules
- Consecutive failures

---

## Central Health Dashboard

Store results in:

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

Dashboard fields:

|Workflow|Status|Health Score|Last Run|Failures|
|---|---|---|---|---|

---

## Daily Health Report

Every morning:

Generate a summary report.

Example:

```text
Total Workflows: 60
Healthy: 52
Warning: 6
Critical: 2
```

Include:

- Failed workflows
- Slow workflows
- Missing executions

Send the report via:

```text
Email
```

or

```text
Slack
```

---

## Alerting System

Immediate alerts for:

### Critical Failure

Example:

```text
Lead Capture Workflow Failed 10 Times
```

---

### Workflow Stopped Running

Example:

```text
No Executions For 24 Hours
```

---

### Credentials Expired

Example:

```text
Google Sheets OAuth Invalid
```

---

Send alerts to:

```text
Slack
```

or

```text
Email
```

---

## Historical Metrics

Store historical health data.

Track:

- Daily health score
- Failure trends
- Runtime trends

The client wants to identify long-term degradation.

---

## Workflow Categorization

Group workflows by:

### Department

- Sales
- Marketing
- Operations
- Finance

---

### Client

- Client A
- Client B
- Client C

This allows filtering reports by category.

---

## Audit Logging

Track:

|Field|Description|
|---|---|
|Detection Time|When issue found|
|Workflow|Affected workflow|
|Issue Type|Failure / Slow / Missing|
|Severity|Warning / Critical|
|Resolution Status|Open / Resolved|

---

## Failure Recovery Suggestions

The dashboard should include recommended actions.

Examples:

### High Failure Rate

Suggestion:

```text
Review recent workflow changes.
```

---

### Missing Executions

Suggestion:

```text
Verify schedule trigger and credentials.
```

---

### Slow Runtime

Suggestion:

```text
Review API response times.
```

---

## Security

The client requires:

- Secure N8N API credentials.
- Restricted access to monitoring data.
- Audit trail of health status changes.

---

## Tools Required

Core Nodes:

- Schedule Trigger
- HTTP Request
- N8N API
- IF Node
- Code Node
- Google Sheets

Optional:

- Airtable
- Notion
- Slack
- Gmail
- PostgreSQL

---

# What The Learner Will Practice

By completing this project, you will learn:

### Monitoring Systems

Observing workflow health.

### Meta-Automation

Building automations that manage automations.

### API Consumption

Using the N8N API.

### Health Scoring

Calculating operational metrics.

### Alerting Systems

Notifying administrators of problems.

### Observability Concepts

Understanding system reliability.

### Production Operations

Managing automation platforms at scale.

---

# Success Criteria

The project is complete when:

- Workflow data is collected automatically.
- Failures are detected.
- Missing executions are detected.
- Performance issues are identified.
- Health scores are calculated.
- Alerts are generated.
- Dashboard data is updated automatically.
- Daily reports are delivered.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — API Health Monitoring Platform

Monitor APIs and external integrations instead of workflows.

---

## Scenario 2 — Server Monitoring Dashboard

Track server uptime, CPU usage, and memory consumption.

---

## Scenario 3 — SaaS Application Health Center

Monitor user signups, payment systems, and service availability.

---

## Scenario 4 — Multi-Client Agency Operations Dashboard

Track automation health separately for each client.

---

## Scenario 5 — AI Workflow Reliability Monitor

Monitor AI agents, token usage, response times, and failure rates.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Real-time monitoring dashboard.
- Workflow dependency mapping.
- Automated incident creation.
- AI-powered anomaly detection.
- Predictive failure analysis.
- Service Level Agreement (SLA) tracking.
- Workflow cost monitoring.
- Credential expiration forecasting.
- Root-cause analysis suggestions.
- Multi-environment monitoring.
- Cross-instance N8N monitoring.
- Auto-remediation workflows.
- Grafana integration.
- Enterprise observability platform.
- Full Operations Center (Ops Center).

---

# Production Insight

This project introduces a key Site Reliability Engineering (SRE) concept:

**Monitor → Detect → Alert → Investigate → Resolve**

You will encounter similar systems in:

- Datadog
- New Relic
- Grafana
- Prometheus
- AWS CloudWatch
- Azure Monitor
- Enterprise Operations Centers

One of the biggest differences between hobby automations and production systems is monitoring. Production teams do not wait for users to report problems. They invest heavily in observability so they can detect failures before business operations are affected. A workflow that silently fails is often more dangerous than one that crashes visibly because nobody knows there is a problem until significant damage has already occurred.