## Project Overview

In this project, you will build an automation that gathers data from multiple sources, calculates business metrics, generates a professional report, and delivers it automatically to stakeholders on a schedule.

This project introduces a very common business automation pattern:

- Data collection
- Data aggregation
- KPI calculation
- Report generation
- Scheduled delivery
- Executive reporting

Nearly every organization needs recurring reports, making this one of the most practical automations you can build.

---

# Client Scenario

## The Client

Sarah manages a digital marketing agency.

Every Monday morning she prepares a weekly performance report for her clients.

To create the report, she manually:

1. Opens multiple spreadsheets.
2. Copies campaign data.
3. Calculates KPIs.
4. Creates a summary.
5. Writes observations.
6. Emails the report to clients.

The process takes several hours every week.

Sarah wants a system that automatically generates and delivers the report before the workday begins.

---

# Business Goal

Every Monday at 8:00 AM:

1. Collect data from multiple sources.
2. Calculate key business metrics.
3. Generate a formatted report.
4. Deliver it via email.
5. Archive a copy for future reference.

The goal is to eliminate repetitive reporting work and provide stakeholders with consistent updates.

---

# Technical Requirements From The Client

## Schedule

Run automatically:

```text
Every Monday at 08:00 AM
```

---

## Data Sources

Read data from:

```text
Google Sheets
```

### Sheet 1 — Sales Data

|Date|Revenue|Orders|
|---|---|---|

### Sheet 2 — Marketing Data

|Date|Ad Spend|Leads|
|---|---|---|

### Sheet 3 — Customer Support Data

|Date|Tickets|Resolved|
|---|---|---|

---

## KPI Calculations

Calculate:

### Sales KPIs

- Total Revenue
- Total Orders
- Average Order Value

### Marketing KPIs

- Total Leads
- Total Ad Spend
- Cost Per Lead

### Support KPIs

- Total Tickets
- Resolution Rate

---

## Executive Summary

Generate a summary section containing:

```text
Weekly Revenue increased by 12% compared to the previous week.

Lead generation remained stable.

Support resolution rate exceeded the target of 90%.
```

Initially this can be manually generated using expressions.

Later it can be generated using AI.

---

## Report Format

Build a professional HTML email.

Include:

### Header

```text
Weekly Business Report
```

### KPI Summary Table

|Metric|Value|
|---|---|

### Key Insights

- Insight 1
- Insight 2
- Insight 3

### Action Items

- Recommendation 1
- Recommendation 2

---

## Recipients

Send the report to:

```text
management@company.com
```

and

```text
stakeholders@company.com
```

---

## Report Archive

Save a copy of the generated report in:

```text
Google Drive
```

Folder:

```text
Weekly Reports
```

---

## Failure Handling

If a data source is unavailable:

- Log the issue
- Notify an administrator

If report generation fails:

- Stop delivery
- Alert the reporting team

If email delivery fails:

- Retry later
- Record the failure

---

## Tools Required

- Schedule Trigger
- Google Sheets Node
- Merge Node
- Code Node
- Set Node
- Gmail Node
- Google Drive Node

Optional:

- OpenAI
- Slack
- Notion

---

# What The Learner Will Practice

By completing this project, you will learn:

### Scheduled Automations

Building workflows that run automatically on a schedule.

### Data Aggregation

Combining data from multiple sources.

### KPI Calculation

Transforming raw data into business metrics.

### Report Generation

Creating structured reports dynamically.

### HTML Email Design

Building professional email layouts.

### Multi-Source Workflows

Working with several systems simultaneously.

### Business Intelligence Fundamentals

Understanding how organizations monitor performance.

---

# Success Criteria

The project is complete when:

- The workflow runs automatically.
- Data is collected from all sources.
- KPIs are calculated correctly.
- Reports are generated successfully.
- Stakeholders receive the report.
- Report archives are stored.
- Failures are logged appropriately.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — E-Commerce Weekly Report

Generate a report containing:

- Revenue
- Orders
- Best-selling products
- Refund statistics

Deliver it to store managers.

---

## Scenario 2 — Social Media Performance Report

Collect metrics from:

- LinkedIn
- X
- Instagram

Calculate:

- Reach
- Engagement
- Follower Growth

---

## Scenario 3 — Recruitment Dashboard Report

Generate a weekly HR report showing:

- Applications received
- Interviews conducted
- Positions filled

---

## Scenario 4 — SaaS Product Analytics Report

Generate a report containing:

- New Users
- Active Users
- Churn Rate
- Subscription Revenue

---

## Scenario 5 — IT Operations Report

Track:

- Server uptime
- System incidents
- Response times
- Infrastructure health

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Generate charts automatically.
- Add AI-generated executive summaries.
- Compare current week vs previous week.
- Build monthly and quarterly reports.
- Deliver reports to Slack.
- Store reports in Notion.
- Create PDF reports.
- Add trend analysis.
- Calculate growth percentages automatically.
- Create personalized reports per department.
- Build a KPI dashboard.
- Add anomaly detection using AI.
- Generate reports for multiple clients.
- Create report approval workflows.
- Build a complete business intelligence reporting system.

---

# Production Insight

This project introduces a core business intelligence pattern:

**Collect → Aggregate → Analyze → Report → Archive**

You will encounter this pattern in:

- Marketing agencies
- SaaS companies
- E-commerce businesses
- Finance departments
- HR teams
- Operations teams
- Executive dashboards

One of the biggest lessons from this project is that stakeholders rarely want raw data. They want insights. The true value of automation is not just gathering information, but transforming it into actionable knowledge that helps decision-makers understand what happened, why it happened, and what they should do next.