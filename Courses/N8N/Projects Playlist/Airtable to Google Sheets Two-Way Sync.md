## Project Overview

In this project, you will build a synchronization system that keeps data in Airtable and Google Sheets aligned automatically.

Whenever a record changes in either system, the workflow detects the change and updates the other system accordingly.

This project introduces one of the most challenging and valuable integration patterns:

- Data synchronization
- Change detection
- Conflict resolution
- State management
- System integration
- Audit logging

Many businesses use multiple tools because different teams prefer different platforms. The challenge is ensuring everyone works with the same data.

---

# Client Scenario

## The Client

Mona runs a recruiting agency.

Her recruiting team manages candidates inside Airtable because they like its database-style interface.

Her management team prefers Google Sheets because it is familiar and easy to share.

Currently, both teams manually update records in their preferred system.

This causes problems:

- Candidate statuses become inconsistent.
- Some updates are missed.
- Reports contain outdated information.
- Team members argue about which system contains the correct data.

Mona wants both systems to stay synchronized automatically.

---

# Business Goal

Whenever data changes:

1. Detect new records.
2. Detect updates.
3. Synchronize changes.
4. Prevent duplicate records.
5. Handle conflicts safely.
6. Maintain an audit trail.

The goal is to allow teams to work in their preferred tool without creating data inconsistencies.

---

# Technical Requirements From The Client

## Systems

Synchronize data between:

```text
Airtable
```

and

```text
Google Sheets
```

---

## Data Structure

Candidate records contain:

|Field|Type|
|---|---|
|Candidate ID|Text|
|Name|Text|
|Email|Email|
|Position|Text|
|Status|Select|
|Updated At|DateTime|

---

## Sync Schedule

Run every:

```text
15 minutes
```

---

## Synchronization Rules

### New Record

If a record exists in Airtable but not in Google Sheets:

- Create it in Google Sheets.

If a record exists in Google Sheets but not in Airtable:

- Create it in Airtable.

---

### Updated Record

If a record exists in both systems:

- Compare timestamps.
- Update the older version.

---

## Unique Identifier

Use:

```text
Candidate ID
```

as the primary key.

Never use:

```text
Row Number
```

or

```text
Record Position
```

as identifiers.

---

## Conflict Detection

A conflict occurs when:

- A record was modified in Airtable.
- The same record was modified in Google Sheets.
- Both changes happened after the last synchronization.

Example:

```text
Airtable:
Status = Interview Scheduled

Google Sheets:
Status = Rejected
```

The system should not overwrite either value automatically.

---

## Conflict Handling

When a conflict is detected:

1. Create a conflict record.
2. Send a notification.
3. Route the record for manual review.

Store conflicts in:

```text
Google Sheets - Conflict Log
```

---

## Audit Logging

Store every sync action.

Example:

|Candidate ID|Action|Source|Timestamp|
|---|---|---|---|
|123|Created|Airtable|10:00|
|456|Updated|Google Sheets|10:05|

---

## Notification System

Send a Slack alert when:

- A conflict occurs.
- A sync fails.

Example:

```text
⚠️ Sync Conflict Detected

Candidate ID: 123
Field: Status

Airtable: Interview Scheduled
Google Sheets: Rejected

Manual review required.
```

---

## Failure Handling

If Airtable is unavailable:

- Log the failure.
- Retry later.

If Google Sheets is unavailable:

- Pause updates.
- Alert administrators.

If synchronization partially succeeds:

- Record successful operations.
- Retry failed records.

---

## Tools Required

- Schedule Trigger
- Airtable Node
- Google Sheets Node
- Code Node
- Merge Node
- IF Node
- Slack Node

Optional:

- Data Store
- Notion
- Gmail

---

# What The Learner Will Practice

By completing this project, you will learn:

### Data Synchronization

Keeping multiple systems aligned automatically.

### Change Detection

Identifying new and modified records.

### Conflict Resolution

Handling competing updates safely.

### Data Modeling

Designing reliable record structures.

### State Tracking

Managing synchronization history.

### Integration Architecture

Building workflows that connect multiple business systems.

### Enterprise Automation Patterns

Learning patterns used in large-scale integrations.

---

# Success Criteria

The project is complete when:

- New records sync correctly.
- Updates sync correctly.
- Duplicate records are prevented.
- Conflicts are detected.
- Conflict notifications work.
- Audit logs are generated.
- Synchronization failures are handled gracefully.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — CRM and Spreadsheet Sync

Synchronize:

- HubSpot
- Google Sheets

Keep customer records aligned.

---

## Scenario 2 — Inventory Management Sync

Synchronize:

- Warehouse database
- Retail inventory sheet

Track stock changes automatically.

---

## Scenario 3 — Student Information Sync

Synchronize:

- School management platform
- Administrative spreadsheets

Maintain consistent student records.

---

## Scenario 4 — Project Management Sync

Synchronize:

- Notion
- Airtable

Keep project tasks aligned.

---

## Scenario 5 — Multi-Branch Customer Database

Synchronize customer records between:

- Branch databases
- Central reporting system

Handle conflicts automatically.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Build near real-time synchronization.
- Add field-level conflict detection.
- Create a conflict resolution dashboard.
- Implement soft deletes.
- Track deleted records.
- Add synchronization metrics.
- Generate sync health reports.
- Support multiple Airtable bases.
- Support multiple spreadsheets.
- Create reusable sync sub-workflows.
- Add record version history.
- Build rollback capabilities.
- Implement batch processing.
- Add data validation before syncing.
- Create a complete integration platform.

---

# Production Insight

This project introduces one of the most difficult integration patterns in software systems:

**Detect → Compare → Resolve → Sync → Audit**

You will encounter this pattern in:

- CRM integrations
- ERP systems
- Data warehouses
- Inventory platforms
- Project management tools
- Enterprise integrations
- SaaS synchronization products

One of the biggest lessons from this project is that synchronization is not simply copying data from one place to another. The real challenge begins when two systems are allowed to modify the same record. This is where concepts such as primary keys, timestamps, conflict detection, audit logs, and reconciliation become critical. Mastering these concepts will help you build integrations that remain reliable even as systems grow in complexity.