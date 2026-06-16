## Project Overview

In this project, you will build a workflow that accepts CSV or Excel files, validates every row, transforms the data into a standardized format, and loads clean records into a destination system.

This is one of the most common automation projects requested by businesses.

Companies frequently receive files from:

- Suppliers
- Clients
- Employees
- Partners
- Legacy Systems

The problem is that incoming files are often messy:

- Missing required fields
- Invalid data types
- Incorrect formats
- Duplicate records
- Inconsistent naming conventions

Before the data can be used, it must be cleaned and validated.

The goal of this project is to build a production-ready ETL (Extract, Transform, Load) pipeline that processes files automatically while providing detailed feedback about errors.

This project introduces several critical concepts:

- Data Validation
- ETL Pipelines
- Schema Enforcement
- Data Transformation
- Error Reporting
- Batch Processing
- Data Quality Management

These concepts are used daily in data engineering, system integration, and enterprise automation.

---

# Client Scenario

## The Client

Amina owns a wholesale distribution company.

Every day, suppliers send inventory updates through Excel files.

Each supplier uses a different format.

Examples:

### Supplier A

```csv
Product Name,Price,Stock
Laptop,1200,50
```

---

### Supplier B

```csv
Name,Cost,Quantity
Laptop,1200,50
```

---

### Supplier C

```csv
Item,Unit Price,Available Units
Laptop,1200,50
```

---

Employees currently review files manually before importing them.

This process takes several hours every week.

Amina wants a workflow that:

- Validates incoming files.
- Rejects invalid rows.
- Standardizes data.
- Loads clean records automatically.

---

# Business Goal

When a file is uploaded:

1. Read the file.
2. Validate every row.
3. Separate valid and invalid records.
4. Transform valid records.
5. Generate an error report.
6. Load clean data into the destination.

The goal is to eliminate manual data cleaning.

---

# Technical Requirements From The Client

## File Submission

Files should be accepted through:

### Option 1

```text
Webhook Upload
```

---

### Option 2

```text
N8N Form Upload
```

---

### Option 3

```text
Google Drive Watch Folder
```

---

Supported formats:

```text
CSV
```

```text
XLSX
```

---

## File Reading

The workflow should:

1. Receive binary file data.
2. Parse the file.
3. Convert rows into items.

Example row:

```json
{
  "product_name": "Laptop",
  "price": "1200",
  "stock": "50"
}
```

---

## Validation Rules

Every row should be validated.

### Product Name

Required.

Cannot be empty.

---

### Price

Required.

Must be numeric.

Example:

```text
1200
```

Valid.

Example:

```text
One Thousand
```

Invalid.

---

### Stock

Required.

Must be an integer.

Example:

```text
50
```

Valid.

Example:

```text
Fifty
```

Invalid.

---

### Duplicate Product IDs

Duplicates should be flagged.

---

### Negative Values

Reject:

```text
Price < 0
```

or

```text
Stock < 0
```

---

## Row Classification

Each row should become:

### Valid Record

Action:

```text
Continue Processing
```

---

### Invalid Record

Action:

```text
Add To Error Report
```

---

## Data Transformation

Standardize incoming data.

Example:

### Supplier A

```json
{
  "Product Name": "Laptop",
  "Price": 1200,
  "Stock": 50
}
```

---

### Supplier B

```json
{
  "Name": "Laptop",
  "Cost": 1200,
  "Quantity": 50
}
```

---

Transform both into:

```json
{
  "product_name": "Laptop",
  "price": 1200,
  "stock": 50
}
```

---

## Destination System

Load valid records into:

```text
Google Sheets
```

or

```text
Airtable
```

or

```text
PostgreSQL
```

or

```text
ERP System
```

---

## Error Report

Generate an error report containing:

|Row Number|Error|
|---|---|
|5|Missing Product Name|
|8|Invalid Price|
|11|Duplicate Product ID|

Store report as:

```text
CSV File
```

or

```text
Excel File
```

---

## Automatic Feedback

After processing:

Send an email containing:

### Summary

```text
500 rows received
```

```text
470 rows imported
```

```text
30 rows rejected
```

---

### Error Report Attachment

Attach the generated file.

---

## Audit Logging

Store:

|Field|Description|
|---|---|
|File Name|Uploaded file|
|Upload Time|Timestamp|
|Total Rows|Count|
|Valid Rows|Count|
|Invalid Rows|Count|
|Processing Duration|Runtime|

Store logs in:

```text
Google Sheets
```

or

```text
Database
```

---

## Failure Handling

If the destination system is unavailable:

### Temporary Failure

Retry automatically.

---

### Permanent Failure

Store the file in:

```text
Manual Review Queue
```

and notify administrators.

---

## Monitoring Dashboard

Track:

|Metric|Description|
|---|---|
|Files Processed|Total uploads|
|Rows Imported|Valid records|
|Rows Rejected|Invalid records|
|Average Processing Time|Performance|
|Failure Rate|Errors|

---

## Security

The client wants:

### File Size Limits

Example:

```text
Maximum 10 MB
```

---

### File Type Validation

Reject:

```text
.exe
```

```text
.zip
```

and unsupported formats.

---

## Tools Required

Core Nodes:

- Webhook
- Form Trigger
- Spreadsheet File Node
- Code Node
- IF Node
- Google Sheets

Optional:

- Airtable
- PostgreSQL
- Slack
- Email

---

# What The Learner Will Practice

By completing this project, you will learn:

### File Processing

Working with uploaded files.

### Binary Data Handling

Managing file uploads inside N8N.

### Data Validation

Checking row-level data quality.

### Data Transformation

Standardizing inconsistent inputs.

### ETL Architecture

Building extract-transform-load pipelines.

### Error Reporting

Providing actionable feedback.

### Data Engineering Fundamentals

Handling real-world business data.

---

# Success Criteria

The project is complete when:

- Files are uploaded successfully.
- Rows are validated.
- Invalid records are separated.
- Valid records are transformed.
- Data is loaded into the destination.
- Error reports are generated.
- Notifications are sent.
- Audit logs are maintained.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Employee Import System

Import employee records into an HR platform.

---

## Scenario 2 — Customer Migration Tool

Process customer exports from a legacy CRM.

---

## Scenario 3 — Accounting Transaction Importer

Validate and import financial transactions.

---

## Scenario 4 — Student Enrollment Processor

Import student registration spreadsheets.

---

## Scenario 5 — Product Catalog Import System

Process supplier product catalogs automatically.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- AI-powered data correction.
- Duplicate detection engine.
- Dynamic schema mapping.
- Multi-file batch processing.
- Supplier-specific transformation rules.
- Data enrichment from external APIs.
- Real-time processing dashboard.
- Automatic rollback on failures.
- Incremental imports.
- Approval workflow before loading.
- Data quality scoring.
- OCR support for scanned documents.
- Multi-tenant file processing.
- Enterprise data ingestion platform.
- Self-service upload portal.

---

# Production Insight

This project introduces a foundational data engineering pattern:

**Receive File → Validate → Transform → Load → Report**

You will encounter similar workflows in:

- ERP systems
- Data warehouses
- Financial platforms
- CRM migrations
- Supply chain systems
- Healthcare systems
- Enterprise integration platforms

One of the biggest lessons from this project is that businesses rarely receive perfectly structured data. Real-world automation often spends more effort validating and cleaning data than actually processing it. A successful automation engineer learns that data quality is not an optional feature—it is a core requirement. A single invalid row can break reports, corrupt databases, or trigger costly business mistakes if validation is not performed properly.