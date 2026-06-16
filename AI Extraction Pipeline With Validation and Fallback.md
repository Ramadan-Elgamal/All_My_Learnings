## Project Overview

In this project, you will build an AI-powered data extraction system that converts unstructured text into structured data while validating the results before they enter downstream systems.

Many businesses receive information through:

- Emails
- Contact forms
- Support tickets
- Chat messages
- PDF documents
- CRM notes

Humans can easily understand this information, but software systems need structured data.

For example, a customer might send:

```text
Hi,

My name is Ahmed Hassan.

I'd like to schedule an appointment next Tuesday.

My phone number is 01012345678.

Thanks.
```

A business system needs:

```json
{
  "name": "Ahmed Hassan",
  "phone": "01012345678",
  "appointment_date": "2026-06-23"
}
```

AI can perform this extraction, but AI is not perfect.

It may:

- Miss fields
- Invent values
- Return invalid JSON
- Misinterpret data
- Produce inconsistent outputs

The goal of this project is to build a reliable extraction pipeline that validates AI outputs, retries when possible, and escalates uncertain cases for human review.

This project teaches one of the most important lessons in AI automation:

**Never trust AI output without verification.**

---

# Client Scenario

## The Client

A property management company receives hundreds of rental inquiries every day.

Prospective tenants send messages through:

- Website forms
- Email
- WhatsApp
- Facebook Messenger

Example inquiry:

```text
Hello,

My name is Sarah Johnson.

I'm interested in the apartment listed on Downtown Street.

I would like to move in around August.

My phone number is 555-123-4567.

My budget is approximately $1,500/month.

Please contact me.

Thank you.
```

Employees manually read every message and enter information into a CRM.

This process is slow and error-prone.

The company wants an AI system that extracts relevant information automatically while ensuring data quality.

---

# Business Goal

When a message arrives:

1. Send the text to an AI model.
2. Extract structured fields.
3. Validate the extracted data.
4. Retry extraction if validation fails.
5. Escalate unresolved cases.
6. Save verified records to the CRM.

The goal is to reduce manual data entry while maintaining accuracy.

---

# Technical Requirements From The Client

## Input Sources

The workflow should accept:

### Gmail

New inquiry emails.

---

### Webhook

Website form submissions.

---

### WhatsApp

Incoming customer messages.

---

### Google Sheets

Imported leads.

---

## Example Input

```text
Hi,

I'm Ahmed.

Looking for a two-bedroom apartment.

Budget around $2000.

Call me at 555-555-1234.

Thanks.
```

---

## AI Extraction Step

Use an LLM to return:

```json
{
  "name": "Ahmed",
  "property_type": "Two Bedroom Apartment",
  "budget": 2000,
  "phone": "555-555-1234"
}
```

The output must be structured JSON.

---

## Target Schema

Required fields:

|Field|Required|
|---|---|
|Name|Yes|
|Phone|Yes|
|Inquiry Type|Yes|
|Budget|No|
|Move-In Date|No|

---

## Validation Layer

Validate extracted data.

### Name

Cannot be empty.

---

### Phone

Must match expected format.

Example:

```text
555-555-1234
```

Valid.

---

### Inquiry Type

Must belong to:

- Rental
- Purchase
- Viewing Request
- General Inquiry

---

### Budget

Must be numeric.

---

## Schema Validation

If AI returns:

```json
{
  "full_name": "Ahmed"
}
```

instead of:

```json
{
  "name": "Ahmed"
}
```

validation should fail.

The client wants strict schema compliance.

---

## First Retry Strategy

If validation fails:

Send a second prompt to the AI.

Example:

```text
Your previous response did not match the required schema.
Return valid JSON with these exact fields:
name, phone, inquiry_type, budget.
```

Attempt extraction again.

---

## Second Retry Strategy

If validation fails again:

Route the record to:

```text
Manual Review Queue
```

---

## Confidence Scoring

The workflow should assign confidence.

Example:

```json
{
  "confidence": 92
}
```

Possible scoring factors:

- Number of fields extracted
- Validation success
- AI self-assessment score

---

## Manual Review Queue

Store unresolved records in:

```text
Google Sheets
```

or

```text
Airtable
```

Required fields:

|Field|Description|
|---|---|
|Original Message|Raw text|
|AI Output|Generated JSON|
|Validation Error|Reason|
|Timestamp|When flagged|

---

## CRM Integration

Validated records should be saved to:

```text
HubSpot
```

or

```text
Salesforce
```

or

```text
Google Sheets
```

---

## Logging

Track:

|Field|Description|
|---|---|
|Request ID|Unique extraction|
|Timestamp|Processing time|
|Validation Result|Pass / Fail|
|Retry Count|Number of attempts|
|Confidence Score|Quality measure|

---

## Alerting

Notify administrators when:

### Excessive Validation Failures

Example:

```text
More than 20 failed extractions today.
```

---

### AI Service Unavailable

Example:

```text
OpenAI API timeout.
```

---

## Monitoring Dashboard

Track:

|Metric|Description|
|---|---|
|Total Extractions|Processed messages|
|Successful Extractions|Passed validation|
|Retry Rate|Needed second attempt|
|Manual Reviews|Human intervention|
|Average Confidence|Extraction quality|

---

## Security

The client requires:

- Secure storage of customer information.
- Protected API credentials.
- Audit trail of extraction decisions.

---

## Tools Required

Core Nodes:

- Gmail Trigger or Webhook
- Basic LLM Chain
- Structured Output Parser
- Code Node
- IF Node
- Google Sheets

Optional:

- HubSpot
- Airtable
- Slack
- PostgreSQL

---

# What The Learner Will Practice

By completing this project, you will learn:

### AI-Powered Data Extraction

Converting text into structured information.

### Schema Validation

Ensuring AI outputs follow strict rules.

### Retry Patterns

Recovering from invalid outputs.

### Confidence Scoring

Measuring AI reliability.

### Human-in-the-Loop Systems

Escalating uncertain cases.

### AI Reliability Engineering

Building dependable AI workflows.

### Production AI Automation

Combining AI with traditional validation logic.

---

# Success Criteria

The project is complete when:

- Incoming text is processed automatically.
- AI extracts structured fields.
- Validation checks run successfully.
- Invalid outputs trigger retries.
- Unresolved cases enter manual review.
- Valid records are saved.
- Logs are generated.
- Monitoring metrics are tracked.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Invoice Data Extraction

Extract invoice numbers, totals, suppliers, and due dates from emails and PDFs.

---

## Scenario 2 — Resume Parsing System

Extract candidate information and skills from uploaded resumes.

---

## Scenario 3 — Customer Support Ticket Classification

Extract category, priority, customer information, and issue summary.

---

## Scenario 4 — Medical Intake Form Processor

Extract patient information from submitted forms and messages.

---

## Scenario 5 — Legal Document Information Extractor

Extract parties, dates, clauses, and obligations from contracts.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Multi-model extraction comparison.
- AI-generated confidence explanations.
- Automatic field correction suggestions.
- OCR integration for scanned documents.
- Multi-language extraction support.
- AI-powered deduplication.
- Feedback loop for improving prompts.
- Extraction quality scoring dashboard.
- Agent-based extraction workflows.
- Vector database storage of source documents.
- Fine-tuned extraction models.
- Self-healing validation prompts.
- Multi-tenant extraction platform.
- Human approval interface.
- Enterprise document processing platform.

---

# Production Insight

This project introduces a foundational AI engineering pattern:

**Input → AI Extraction → Validation → Retry → Human Review → Storage**

You will encounter similar architectures in:

- Insurance claim processing
- CRM lead management
- Document automation systems
- Customer support platforms
- Financial services
- Healthcare administration
- Enterprise AI products

A common beginner mistake is assuming that if an AI model returns an answer, the answer is correct. Production AI systems rarely trust model outputs directly. Instead, they surround AI with validation layers, fallback strategies, confidence checks, and human review processes. The AI becomes one component of a larger reliability system rather than the sole source of truth. This approach dramatically reduces errors while still capturing the efficiency benefits of automation.