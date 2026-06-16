## Project Overview

In this project, you will build a workflow that receives data from multiple sources, detects duplicate records, and ensures that only unique records are stored.

Duplicate data is one of the most common problems businesses face. A single customer may appear multiple times because they filled out several forms, signed up through different channels, or were imported from multiple systems.

Poor deduplication leads to:

- Duplicate CRM contacts
- Repeated email campaigns
- Incorrect reports
- Inflated metrics
- Poor customer experience

The goal of this project is to build a reliable deduplication pipeline that identifies duplicates before they reach the destination system while maintaining an audit trail of every decision.

This project introduces important data engineering concepts:

- Data Quality
- Deduplication Strategies
- Data Validation
- Data Merging
- Audit Logging
- Unique Identifiers
- Concurrent Processing Challenges

This is a common requirement in CRM integrations, marketing automation, reporting systems, and data migration projects.

---

# Client Scenario

## The Client

Hassan owns a real estate agency.

Leads enter the business from multiple sources:

- Facebook Lead Ads
- Website Forms
- WhatsApp Campaigns
- Referral Forms
- Property Listing Portals

The same person often appears multiple times.

Example:

```text
Ahmed Hassan
ahmed@gmail.com
```

might submit:

- A property inquiry
- A mortgage inquiry
- A consultation request

Without deduplication, the CRM fills with duplicate records.

Sales agents accidentally contact the same person multiple times, creating a poor customer experience.

Hassan wants a system that automatically detects duplicates and stores only clean data.

---

# Business Goal

When data arrives:

1. Validate incoming records.
2. Compare against existing records.
3. Detect duplicates.
4. Save only unique records.
5. Log duplicate decisions.
6. Provide visibility into skipped records.

The goal is to maintain a clean customer database.

---

# Technical Requirements From The Client

## Data Sources

The workflow should combine data from multiple sources.

Examples:

```text
Facebook Lead Ads
```

```text
Website Forms
```

```text
Google Sheets Imports
```

```text
CSV Uploads
```

Example incoming data:

```json
{
  "name": "Ahmed Hassan",
  "email": "ahmed@gmail.com",
  "phone": "+201234567890"
}
```

---

## Data Consolidation

Merge incoming records into a single processing pipeline.

Use:

```text
Merge Node
```

to create a unified stream of records.

---

## Deduplication Rules

The client wants duplicates identified by:

### Primary Key

```text
Email Address
```

---

### Secondary Key

```text
Phone Number
```

---

### Optional Fallback

```text
National ID
```

or

```text
CRM Customer ID
```

---

## Record Classification

Every record should be classified as:

### New Record

Never seen before.

Action:

```text
Insert Into CRM
```

---

### Duplicate Record

Already exists.

Action:

```text
Skip Insert
```

and

```text
Log Duplicate
```

---

## Duplicate Logging

Store duplicate records in:

```text
Google Sheets
```

Fields:

|Field|Description|
|---|---|
|Record ID|Incoming record|
|Duplicate Key|Matched field|
|Existing Record ID|Existing contact|
|Source|Origin system|
|Timestamp|Detection time|

---

## Destination System

Store unique records in:

```text
CRM
```

or

```text
Google Sheets
```

or

```text
Airtable
```

---

## Data Quality Validation

Before deduplication:

Validate:

### Email Format

Example:

```text
user@example.com
```

---

### Phone Format

Example:

```text
+201234567890
```

---

### Required Fields

- Name
- Email
- Phone

Invalid records should be routed to:

```text
Validation Error Queue
```

---

## Audit Trail

Track every decision.

Example log:

|Record|Result|Reason|
|---|---|---|
|Ahmed|Duplicate|Email Match|
|Sara|New|No Match Found|

Store logs in:

```text
Google Sheets
```

---

## Reporting

Generate weekly reports:

|Metric|Description|
|---|---|
|Total Records Received|Incoming records|
|Unique Records Saved|Accepted records|
|Duplicates Found|Rejected duplicates|
|Validation Errors|Invalid records|
|Duplicate Rate|Percentage duplicates|

Deliver reports via:

```text
Email
```

or

```text
Slack
```

---

## Concurrent Processing Protection

The client occasionally receives large lead batches.

The workflow should prevent:

```text
Race Conditions
```

Example:

Two identical records arrive at the same moment.

Only one should be inserted.

The second should be marked as duplicate.

---

## Failure Handling

If the destination CRM is unavailable:

- Retry insertion.
- Preserve record state.
- Alert administrators.

If duplicate checking fails:

- Route to manual review queue.

---

## Tools Required

Core Nodes:

- Merge Node
- IF Node
- Code Node
- Google Sheets
- Airtable
- CRM Integration

Optional:

- Redis
- PostgreSQL
- Data Store
- Slack

---

# What The Learner Will Practice

By completing this project, you will learn:

### Deduplication Design

Choosing appropriate uniqueness rules.

### Data Validation

Improving incoming data quality.

### Data Consolidation

Combining records from multiple systems.

### Audit Logging

Tracking workflow decisions.

### Data Quality Engineering

Building reliable pipelines.

### Concurrent Processing Awareness

Understanding race conditions.

### CRM Integration Patterns

Keeping business data clean.

---

# Success Criteria

The project is complete when:

- Multiple data sources feed the workflow.
- Duplicate records are detected.
- Unique records are stored.
- Duplicates are logged.
- Validation errors are separated.
- Reports are generated.
- Audit logs exist.
- Concurrent duplicate inserts are prevented.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — E-Commerce Customer Database Cleanup

Merge customer records from multiple sales channels while removing duplicates.

---

## Scenario 2 — Newsletter Subscriber Management

Prevent duplicate subscribers across multiple signup forms.

---

## Scenario 3 — Recruitment Candidate Pipeline

Detect duplicate candidates applying through multiple job boards.

---

## Scenario 4 — Event Registration System

Prevent attendees from registering multiple times.

---

## Scenario 5 — Healthcare Patient Registry

Ensure patients have only one record across multiple clinics.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Fuzzy matching for names.
- Duplicate confidence scoring.
- AI-assisted duplicate detection.
- Automatic record merging.
- Master customer profiles.
- Multi-source identity resolution.
- Real-time deduplication dashboard.
- Historical duplicate analysis.
- Data quality scoring.
- Duplicate review workflow.
- Merge conflict handling.
- Large-scale batch processing.
- Cross-system deduplication.
- Data warehouse integration.
- Enterprise customer identity platform.

---

# Production Insight

This project introduces a pattern used throughout data engineering and CRM systems:

**Receive → Validate → Compare → Classify → Store → Log**

You will encounter similar architectures in:

- CRM platforms
- Marketing automation tools
- Customer data platforms (CDPs)
- Data warehouses
- E-commerce systems
- Healthcare systems
- Enterprise integrations

One of the most important lessons from this project is that data quality problems become exponentially more expensive to fix once bad data enters a system. A duplicate customer record may seem harmless at first, but it can affect reporting, marketing campaigns, customer support, sales activities, and business decisions. The best place to solve data quality problems is at the point where data enters the system, before those problems spread downstream.