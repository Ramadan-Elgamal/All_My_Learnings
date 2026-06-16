## Project Overview

In this project, you will build an automation that continuously monitors websites and immediately alerts a team when a website becomes unavailable or starts returning errors.

The workflow will periodically check a list of URLs, evaluate their responses, and notify stakeholders when problems are detected.

This project introduces one of the most important DevOps and operations automation patterns:

- Monitoring
- Health checks
- Incident detection
- Alerting
- State management
- Reliability engineering

Many businesses rely on website uptime for revenue, making monitoring systems critical infrastructure.

---

# Client Scenario

## The Client

Omar owns a small agency that manages websites for several clients.

One morning, a client calls angrily because their online store was offline for six hours before anyone noticed.

The agency loses credibility because there was no monitoring system in place.

Currently, Omar's team manually checks websites throughout the day, which is unreliable and doesn't scale.

He wants an automated monitoring system that detects downtime immediately and alerts the team before clients notice.

---

# Business Goal

Every few minutes:

1. Check a list of websites.
2. Verify they are responding correctly.
3. Detect outages and errors.
4. Notify the operations team.
5. Avoid sending duplicate alerts repeatedly.
6. Keep a history of incidents.

The goal is to reduce downtime and improve response times.

---

# Technical Requirements From The Client

## Monitoring Schedule

Run every:

```text
5 minutes
```

---

## Website List

Store monitored websites in:

```text
Google Sheets
```

Example:

|Website Name|URL|
|---|---|
|Main Website|https://example.com|
|Store|https://shop.example.com|
|Blog|https://blog.example.com|

---

## Health Check

For each URL:

1. Send an HTTP request.
2. Capture:
    - Status Code
    - Response Time
    - Timestamp

---

## Healthy Conditions

A website is considered healthy if:

```text
Status Code = 200
```

and

```text
Response Time < 5 seconds
```

---

## Failure Conditions

Trigger an alert if:

- Status code is not 200.
- Request times out.
- DNS lookup fails.
- SSL errors occur.
- Response time exceeds threshold.

---

## Incident Logging

Save all failures to:

```text
Google Sheets
```

Columns:

|Website|Status Code|Response Time|Error|Timestamp|
|---|---|---|---|---|

---

## Alerting

Send a Slack notification to:

```text
#website-alerts
```

Example:

```text
🚨 Website Alert

Website: shop.example.com
Status: 500 Internal Server Error
Response Time: 8.2 seconds

Detected At:
2026-06-15 14:25 UTC
```

---

## Cooldown System

After an alert is sent:

Do not send another alert for the same issue for:

```text
30 minutes
```

This prevents alert spam.

---

## Recovery Notification

When the website becomes healthy again:

Send:

```text
✅ Website Recovered

Website: shop.example.com

Status: Healthy
Response Time: 1.1 seconds
```

---

## Tools Required

- Schedule Trigger
- HTTP Request Node
- Google Sheets Node
- IF Node
- Slack Node
- Set Node

Optional:

- Gmail
- Airtable
- Notion
- Data Store

---

# What The Learner Will Practice

By completing this project, you will learn:

### Monitoring Systems

Building systems that continuously check infrastructure health.

### HTTP Requests

Working with web requests and status codes.

### Incident Detection

Identifying failures automatically.

### Alerting Systems

Notifying teams when issues occur.

### State Management

Tracking current website status.

### Cooldown Logic

Preventing alert fatigue.

### DevOps Fundamentals

Learning operational reliability patterns.

---

# Success Criteria

The project is complete when:

- Websites are checked automatically.
- Failures are detected accurately.
- Alerts are delivered successfully.
- Recovery notifications work.
- Incident history is stored.
- Duplicate alert spam is prevented.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — API Monitoring System

Monitor API endpoints.

Track:

- Status Codes
- Response Times
- Error Rates

Alert developers when issues occur.

---

## Scenario 2 — Internal Service Monitoring

Monitor:

- Authentication Service
- Payment Service
- Notification Service

Notify engineering teams of outages.

---

## Scenario 3 — Third-Party Vendor Monitoring

Monitor external providers such as:

- Payment gateways
- Shipping APIs
- CRM systems

Alert operations when dependencies fail.

---

## Scenario 4 — SSL Certificate Expiration Monitor

Check website certificates.

Alert administrators when certificates are nearing expiration.

---

## Scenario 5 — Uptime Monitoring for Client Websites

Monitor dozens of client websites.

Generate daily uptime reports.

Notify support teams of incidents.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Track response-time trends.
- Build uptime percentage calculations.
- Create daily uptime reports.
- Monitor website content changes.
- Add SMS alerts.
- Integrate with Telegram.
- Create severity levels for incidents.
- Build a monitoring dashboard.
- Add multi-region health checks.
- Monitor SSL certificate expiration.
- Create maintenance windows.
- Add automatic escalation rules.
- Monitor APIs and webhooks.
- Generate incident reports.
- Build a complete observability platform.

---

# Production Insight

This project introduces a foundational reliability engineering pattern:

**Monitor → Detect → Alert → Respond → Recover**

You will encounter this pattern in:

- SaaS companies
- E-commerce platforms
- Hosting providers
- DevOps teams
- IT operations departments
- Managed service providers
- Enterprise infrastructure teams

One of the most important lessons from this project is that monitoring is not about detecting failures—it is about detecting failures early enough to take action. Many businesses discover outages through customer complaints, which means the monitoring process has already failed. Effective monitoring gives teams visibility before customers are impacted, turning reactive support into proactive operations.