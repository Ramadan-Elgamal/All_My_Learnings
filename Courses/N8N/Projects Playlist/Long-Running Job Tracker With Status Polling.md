## Project Overview

In this project, you will build a system that accepts long-running tasks, processes them asynchronously, and allows clients to check progress using a status endpoint.

Many operations take longer than a typical HTTP request can handle:

- AI document analysis
- Video processing
- Large file imports
- Report generation
- Bulk email campaigns
- Data synchronization

A common beginner mistake is trying to perform all processing inside a single webhook request.

Example:

```text
Client → Webhook → Process 10,000 Records → Return Response
```

This often leads to:

- HTTP timeouts
- Failed executions
- Poor user experience
- Unreliable systems

Professional systems use asynchronous processing.

Instead of waiting for completion:

1. Accept the request.
2. Create a job.
3. Return a Job ID immediately.
4. Process the task in the background.
5. Allow clients to check status later.

This project teaches a common backend architecture pattern used by modern APIs.

---

# Client Scenario

## The Client

Nadia owns a document processing company.

Customers upload PDF files that contain:

- Contracts
- Invoices
- Reports
- Legal documents

After upload, an AI system:

1. Reads the PDF.
2. Extracts information.
3. Classifies the document.
4. Generates a summary.
5. Saves results.

Processing may take:

```text
2–10 Minutes
```

Sometimes even longer.

Customers currently submit files and wait for a response.

The system frequently times out.

Users often resubmit the same file because they think the upload failed.

This creates duplicate work and confusion.

Nadia wants a proper job-tracking system.

---

# Business Goal

When a file is submitted:

1. Create a job.
2. Return a Job ID immediately.
3. Process the file asynchronously.
4. Track progress.
5. Allow users to check status.
6. Return results when complete.

The goal is to provide a reliable experience for long-running operations.

---

# Technical Requirements From The Client

## Job Submission Endpoint

Create:

```http
POST /jobs
```

Request example:

```json
{
  "file_url": "https://example.com/invoice.pdf"
}
```

---

## Immediate Response

The endpoint should NOT wait for processing.

Instead return:

```json
{
  "job_id": "job_12345",
  "status": "queued"
}
```

Response time should be under:

```text
2 Seconds
```

---

## Job ID Generation

Each submission must receive a unique ID.

Example:

```text
job_12345
job_12346
job_12347
```

Possible strategies:

- UUID
- Timestamp + Random Number
- Auto Increment ID

---

## Job Storage

Store jobs in:

- Google Sheets
- Airtable
- Data Store
- PostgreSQL

Required fields:

|Field|Description|
|---|---|
|Job ID|Unique identifier|
|Status|Current state|
|Created At|Submission time|
|Updated At|Last update|
|Progress|Percentage|
|Result URL|Output location|
|Error Message|Failure reason|

---

## Job States

Supported states:

### Queued

```text
Waiting To Start
```

---

### Running

```text
Currently Processing
```

---

### Completed

```text
Finished Successfully
```

---

### Failed

```text
Processing Error
```

---

### Cancelled

```text
Stopped By User
```

---

## Background Processing Workflow

After job creation:

1. Launch a separate workflow.
2. Perform processing.
3. Update status throughout execution.

Example:

```text
Queued → Running → Completed
```

---

## Progress Tracking

The client wants visibility into progress.

Example:

```json
{
  "progress": 65
}
```

Possible stages:

|Stage|Progress|
|---|---|
|Uploaded|10%|
|Reading File|25%|
|Extracting Data|50%|
|Generating Summary|80%|
|Completed|100%|

---

## Status Endpoint

Create:

```http
GET /jobs/{job_id}
```

Example response:

```json
{
  "job_id": "job_12345",
  "status": "running",
  "progress": 65
}
```

---

## Completed Job Response

Example:

```json
{
  "job_id": "job_12345",
  "status": "completed",
  "progress": 100,
  "result_url": "https://storage.example.com/result.pdf"
}
```

---

## Failed Job Response

Example:

```json
{
  "job_id": "job_12345",
  "status": "failed",
  "error": "Unable to process PDF"
}
```

---

## Polling Support

Clients will repeatedly call:

```http
GET /jobs/{job_id}
```

until completion.

The workflow should handle frequent status requests efficiently.

---

## Duplicate Submission Detection

If the same file is submitted twice:

```text
invoice.pdf
invoice.pdf
```

The system should detect duplicates.

Possible action:

```text
Return Existing Job
```

instead of creating a new one.

---

## Cancellation Endpoint

Create:

```http
POST /jobs/{job_id}/cancel
```

Behavior:

- Mark job as cancelled.
- Stop processing if possible.

---

## Result Storage

Completed outputs may be stored in:

- Google Drive
- S3-compatible storage
- Dropbox
- Notion
- Database

Store a reference in the job record.

---

## Audit Logging

Track:

|Field|Description|
|---|---|
|Job ID|Unique job|
|Submission Time|When created|
|Completion Time|When finished|
|Duration|Total runtime|
|Status|Final state|

---

## Monitoring Dashboard

Track:

|Metric|Description|
|---|---|
|Jobs Submitted|Total|
|Jobs Completed|Success|
|Jobs Failed|Errors|
|Average Processing Time|Performance|
|Queue Length|Backlog|

---

## Security

The client requires:

- Authentication for job submission.
- Access control on status endpoints.
- Secure storage of uploaded files.
- Audit trail of all job activity.

---

## Tools Required

Core Nodes:

- Webhook
- Code Node
- Execute Workflow
- IF Node
- Google Sheets
- Respond to Webhook

Optional:

- PostgreSQL
- Airtable
- Redis
- Google Drive
- S3

---

# What The Learner Will Practice

By completing this project, you will learn:

### Asynchronous Processing

Handling long-running operations.

### Job Queue Patterns

Managing background work.

### State Management

Tracking progress and status.

### API Design

Building submission and status endpoints.

### Workflow Coordination

Connecting multiple workflows.

### Reliability Engineering

Preventing timeouts and duplicate processing.

### Backend Architecture

Implementing production-grade job systems.

---

# Success Criteria

The project is complete when:

- Jobs can be submitted.
- Unique job IDs are generated.
- Background processing works.
- Status updates are stored.
- Polling endpoint returns progress.
- Completed jobs return results.
- Failed jobs return errors.
- Monitoring metrics are collected.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — AI Video Processing Service

Upload videos and track transcription, summarization, and rendering progress.

---

## Scenario 2 — Bulk Email Campaign Manager

Submit large campaigns and monitor sending status.

---

## Scenario 3 — Large CSV Import System

Upload thousands of records and track import progress.

---

## Scenario 4 — Report Generation Platform

Generate complex financial reports and monitor completion.

---

## Scenario 5 — Image Processing Pipeline

Submit image batches for resizing, tagging, and optimization.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Real queue management with Redis.
- Priority job processing.
- Concurrent worker execution.
- WebSocket live status updates.
- Callback URL notifications.
- Retry failed jobs automatically.
- Scheduled job execution.
- Distributed worker architecture.
- Job dependency chains.
- Estimated completion time prediction.
- Multi-tenant job processing.
- AI-powered queue optimization.
- Rate-limited worker pools.
- Workflow orchestration engine.
- Full task-processing platform.

---

# Production Insight

This project introduces a common architecture used by modern APIs:

**Submit Job → Queue Job → Process Asynchronously → Track Status → Deliver Results**

You will encounter similar patterns in:

- AI platforms
- Video processing services
- Cloud storage providers
- Data analytics platforms
- Document processing systems
- Enterprise workflow engines

Examples include services such as batch processing APIs, long-running operations, and asynchronous processing services.

A common mistake is designing APIs around synchronous execution. This works for small tasks but quickly breaks when processing time increases. Professional systems separate request acceptance from task execution. Users receive immediate feedback, servers remain responsive, and long-running operations can be monitored, retried, cancelled, and audited independently.