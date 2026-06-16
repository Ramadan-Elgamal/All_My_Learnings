## Project Overview

In this project, you will build an automation that monitors a Google Drive folder and notifies a team whenever a new file is uploaded.

The workflow continuously checks a specific folder, detects newly added files, prevents duplicate notifications, and alerts users through Slack or email.

This project introduces a very common automation pattern used in document-driven businesses:

- File monitoring
- State management
- Deduplication
- Notifications
- Polling strategies
- Business process automation

Many companies rely on workflows like this to ensure that important documents never go unnoticed.

---

# Client Scenario

## The Client

Mona runs an accounting firm.

Her clients regularly upload documents such as:

- Invoices
- Tax forms
- Bank statements
- Contracts

to a shared Google Drive folder.

The problem is that her team has no way of knowing when a client uploads something new.

Employees constantly:

- Refresh Google Drive
- Check folders manually
- Send messages asking if documents have arrived

Sometimes important files remain unnoticed for hours or even days.

Mona wants an automated notification system that immediately informs the team whenever a client uploads a new document.

---

# Business Goal

Whenever a new file appears in a specific Google Drive folder:

1. Detect the new file.
2. Determine whether it has already been processed.
3. Send a notification.
4. Include useful file details.
5. Avoid duplicate alerts.

The goal is to create visibility around incoming documents without requiring manual monitoring.

---

# Technical Requirements From The Client

## Folder Monitoring

Monitor the folder:

```text
Client Uploads
```

The workflow should periodically check for newly uploaded files.

---

## Notification Information

Each notification should contain:

- File name
- Upload date
- File type
- File owner/uploader (if available)
- Direct Google Drive link

Example:

```text
📄 New File Uploaded

File Name: April-Invoice.pdf
File Type: PDF
Uploaded At: 2026-06-15 14:22

Open File:
https://drive.google.com/...
```

---

## Notification Destination

Send notifications to:

### Option A

Slack channel:

```text
#client-documents
```

### Option B

Accounting team email address:

```text
accounting@company.com
```

---

## Duplicate Prevention

The client only wants notifications once.

If the workflow runs every few minutes:

- Previously detected files should not trigger again.
- Processed files must be tracked.

Store processed file IDs inside:

- Google Sheets
- Airtable
- Data Store
- Another state storage solution

---

## Schedule Requirements

Run every:

```text
5 minutes
```

---

## Failure Handling

If Google Drive is temporarily unavailable:

- Retry later
- Continue normal operation when access returns

If notifications fail:

- Log the error
- Alert the administrator

---

## Tools Required

- Schedule Trigger
- Google Drive Node
- IF Node
- Slack Node or Gmail Node

Optional:

- Google Sheets
- Airtable
- Data Store
- Set Node

---

# What The Learner Will Practice

By completing this project, you will learn:

### Polling Workflows

How to repeatedly check external systems for changes.

### Google Drive Integration

Working with folders and files.

### Deduplication Logic

Preventing duplicate processing.

### State Management

Tracking what has already been processed.

### Notifications

Delivering useful information to users.

### Production Thinking

Designing workflows that run continuously.

### File-Based Automation

Building automations around document workflows.

---

# Success Criteria

The project is complete when:

- The workflow checks Google Drive automatically.
- New files are detected.
- Notifications are delivered successfully.
- Duplicate notifications never occur.
- File information is displayed clearly.
- The workflow can run indefinitely.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — HR Resume Monitoring

An HR department wants notifications whenever candidates upload resumes.

Folder:

```text
Candidate Applications
```

Notify:

```text
#recruitment
```

Include:

- Candidate name
- Resume file
- Submission date

---

## Scenario 2 — School Assignment Submission Tracker

Teachers want to know when students upload assignments.

Folder:

```text
Student Assignments
```

Notify:

```text
#teachers
```

Include:

- Student name
- Assignment name
- Upload date

---

## Scenario 3 — Legal Contract Intake System

A law firm receives client contracts through Google Drive.

Folder:

```text
Incoming Contracts
```

Notify:

```text
#legal-team
```

Include:

- Contract name
- Client name
- Upload date

---

## Scenario 4 — Marketing Asset Review Queue

Designers upload marketing assets for approval.

Folder:

```text
Marketing Reviews
```

Notify:

```text
#creative-review
```

Include:

- Asset name
- Designer
- File type

---

## Scenario 5 — Real Estate Document Processing

Agents upload property documents to a shared folder.

Folder:

```text
Property Documents
```

Notify:

```text
#real-estate-ops
```

Include:

- Property ID
- Document type
- Upload date

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Notify different channels based on file type.
- Automatically move files to another folder after processing.
- Generate AI summaries for uploaded documents.
- Extract text from PDFs automatically.
- Create a Notion record for every uploaded file.
- Create a Google Sheets audit log.
- Detect duplicate files based on filename or hash.
- Send different notifications based on uploader.
- Create a dashboard showing upload statistics.
- Trigger approval workflows for certain document types.
- Automatically rename files according to company standards.
- Generate thumbnails for uploaded images.
- Perform virus scanning before notifying users.
- Route documents to different teams automatically.
- Build a complete document intake pipeline.

---

# Production Insight

This project introduces a pattern that appears constantly in business automation:

**Monitor → Detect Change → Deduplicate → Notify**

You will see this pattern in:

- File monitoring systems
- Inventory tracking
- Database synchronization
- Security monitoring
- Customer onboarding
- Compliance auditing
- Data ingestion pipelines

A key lesson from this project is that many real-world systems are not triggered by events directly. Instead, they rely on periodic checks and intelligent tracking of what has already been processed.