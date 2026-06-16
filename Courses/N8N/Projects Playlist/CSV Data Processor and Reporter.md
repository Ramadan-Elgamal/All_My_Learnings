## Project Overview

In this project, you will build a workflow that accepts a CSV file, processes its contents, applies business rules and transformations, and generates a summary report.

Many businesses receive CSV files from customers, suppliers, employees, accounting systems, or third-party software. Before the data can be used, it often needs validation, cleaning, calculations, and reporting.

This project introduces learners to file processing workflows and teaches how N8N handles binary files and structured data.

You will learn:

- File uploads
- Binary data handling
- CSV parsing
- Data transformation
- Aggregation and reporting
- Error handling
- Data quality validation

This is one of the most common freelance automation projects because many organizations still exchange data through spreadsheets and CSV exports.

---

# Client Scenario

## The Client

Fatma owns a chain of retail stores.

Every evening, each store exports its sales data as a CSV file and uploads it to a company portal.

The CSV contains:

- Products sold
- Quantities
- Unit prices
- Store locations

Currently, Fatma's team manually:

1. Downloads the file.
2. Opens Excel.
3. Calculates totals.
4. Identifies data issues.
5. Creates a daily sales summary.
6. Emails the report to management.

This process takes significant time every day.

Fatma wants the entire process automated.

---

# Business Goal

Whenever a CSV file is submitted:

1. Receive the file.
2. Parse the data.
3. Validate each row.
4. Calculate key metrics.
5. Generate a summary report.
6. Email the report to management.

The goal is to eliminate manual spreadsheet work and provide faster insights.

---

# Technical Requirements From The Client

## File Submission

The workflow should accept a CSV file through:

- A Webhook
- An N8N Form
- A File Upload Form

---

## Sample CSV Structure

```csv
Store,Product,Quantity,UnitPrice
Cairo,Keyboard,5,20
Alexandria,Mouse,10,15
Cairo,Monitor,2,150
```

---

## Validation Rules

Each row must contain:

- Store Name
- Product Name
- Quantity
- Unit Price

Reject rows that:

- Have missing values
- Contain invalid numbers
- Have negative quantities
- Have negative prices

Invalid rows should be reported separately.

---

## Calculations Required

For every row:

```text
Revenue = Quantity × Unit Price
```

Calculate:

- Total Revenue
- Total Orders
- Total Quantity Sold
- Revenue By Store

---

## Report Requirements

Management should receive:

```text
Daily Sales Report

Total Revenue: $4,250
Total Orders: 120
Total Items Sold: 450

Top Store:
Cairo

Invalid Records:
3
```

---

## Email Delivery

Send the report automatically to:

```text
management@company.com
```

---

## Failure Handling

If the CSV format is invalid:

- Reject the file
- Send an error notification

If some rows are invalid:

- Continue processing valid rows
- Include invalid rows in the report

---

## Tools Required

- Webhook or Form Trigger
- CSV Parser
- Code Node
- Set Node
- Gmail Node

Optional:

- Google Sheets
- Slack Node
- Notion Node

---

# What The Learner Will Practice

By completing this project, you will learn:

### Binary File Handling

How N8N manages uploaded files.

### CSV Processing

Reading and parsing CSV data.

### Data Validation

Checking data quality before processing.

### Transformations

Calculating new values from existing data.

### Aggregation

Summarizing large datasets.

### Reporting

Generating business-friendly summaries.

### Defensive Automation

Handling bad input gracefully.

---

# Success Criteria

The project is complete when:

- CSV files are accepted successfully.
- Rows are parsed correctly.
- Invalid rows are detected.
- Revenue calculations are accurate.
- Summary metrics are generated.
- The report is emailed automatically.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Employee Timesheet Processor

Employees upload weekly timesheets.

CSV Columns:

- Employee Name
- Hours Worked
- Department
- Hourly Rate

Generate:

- Payroll totals
- Overtime calculations
- Department summaries

---

## Scenario 2 — Inventory Import Validator

A warehouse receives inventory updates through CSV files.

CSV Columns:

- SKU
- Product Name
- Stock Quantity
- Warehouse

Generate:

- Inventory summary
- Invalid SKU report
- Low stock alerts

---

## Scenario 3 — Student Exam Results Analyzer

A school uploads exam results.

CSV Columns:

- Student Name
- Subject
- Score

Generate:

- Average score
- Top performers
- Failed students list

---

## Scenario 4 — Marketing Campaign Report Generator

A marketing agency uploads campaign performance exports.

CSV Columns:

- Campaign
- Clicks
- Impressions
- Cost

Generate:

- CTR calculations
- Cost summaries
- Top campaigns

---

## Scenario 5 — Supplier Invoice Processor

Suppliers upload invoice data.

CSV Columns:

- Invoice Number
- Supplier
- Amount
- Due Date

Generate:

- Payment schedule
- Outstanding totals
- Validation report

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Support Excel (.xlsx) files in addition to CSV.
- Save processed data into Google Sheets.
- Save processed data into Airtable.
- Create charts and graphs automatically.
- Generate a PDF report instead of an email.
- Send a Slack notification after processing.
- Use AI to identify unusual sales patterns.
- Create a dashboard in Notion.
- Archive processed files in Google Drive.
- Generate separate reports per store.
- Detect duplicate records automatically.
- Build a reusable validation engine using configuration rules.
- Add support for multiple CSV formats.
- Create a historical reporting database.
- Generate executive summaries using AI.

---

# Production Insight

This project introduces a pattern that appears in countless business automations:

**Receive File → Validate → Transform → Aggregate → Report**

You will find this pattern in:

- Financial reporting systems
- Payroll processing
- Inventory management
- Compliance reporting
- Data migration projects
- Business intelligence workflows
- ETL (Extract, Transform, Load) pipelines

A large percentage of automation consulting projects involve taking messy spreadsheet exports and turning them into reliable business information. Learning this pattern will prepare you for many real-world client requests.