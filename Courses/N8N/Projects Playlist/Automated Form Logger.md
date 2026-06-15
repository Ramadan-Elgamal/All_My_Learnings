## Project Overview

In this project, you will build your first complete N8N automation.

A user submits a form, and N8N automatically stores the submitted information inside a Google Sheets spreadsheet.

While the workflow itself is simple, it introduces some of the most important concepts in N8N:

- Triggers
- Data flow
- Items
- Field mapping
- Data transformation
- Basic validation
- Working with Google Sheets

This project intentionally focuses on understanding how data moves through a workflow rather than solving a complex business problem.

---

# Client Scenario

## The Client

Sarah is a freelance web designer.

She recently launched a portfolio website to attract new clients. Visitors can fill out a "Request a Quote" form to inquire about projects.

Currently, every inquiry is sent to Sarah's email inbox.

As her business grows, managing inquiries through email has become difficult:

- Leads get buried in long email threads
- Some inquiries are accidentally missed
- There is no easy way to track all leads in one place
- She cannot quickly sort or filter inquiries

Sarah wants every form submission automatically stored in a spreadsheet so she can manage leads more efficiently.

---

# Business Goal

The goal is to create a centralized lead database.

Whenever a visitor submits the website form:

1. The information should be captured automatically.
2. The data should be validated.
3. The submission should be added as a new row in Google Sheets.
4. Sarah should be able to open the spreadsheet at any time and see all inquiries.

No manual data entry should be required.

---

# Technical Requirements From The Client

### Form Fields

The client wants the form to contain:

- Full Name
- Email Address
- Phone Number
- Project Type
- Budget Range
- Message

---

### Validation Rules

Before saving the data:

- Name cannot be empty
- Email cannot be empty
- Email should look like a valid email address
- Message cannot be empty

If validation fails:

- The workflow should not save the submission

---

### Google Sheet Structure

The spreadsheet should contain the following columns:

|Column|
|---|
|Submission Date|
|Full Name|
|Email|
|Phone|
|Project Type|
|Budget Range|
|Message|

Each form submission should create a new row.

---

### Tools Required

- N8N Form Trigger
- Set Node
- Google Sheets Node

Optional:

- IF Node for validation

---

# What The Learner Will Practice

By completing this project, you will learn:

### Form Trigger

How workflows start when a user submits a form.

### Data Flow

How submitted form values move between nodes.

### Items

Understanding how N8N represents data internally.

### Mapping

Connecting form fields to spreadsheet columns.

### Data Transformation

Using the Set node to reshape data before storage.

### Validation

Preventing bad data from entering your system.

### Google Sheets Integration

Writing data to an external application.

---

# Success Criteria

The project is complete when:

- A user submits the form.
- The workflow executes successfully.
- Validation passes.
- A new row appears in Google Sheets.
- All fields are mapped correctly.
- No manual work is required.

---

# Alternative Scenarios For Practice

After finishing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Clinic Appointment Requests

A small clinic wants patients to submit appointment requests online.

Form Fields:

- Patient Name
- Phone Number
- Email
- Preferred Date
- Preferred Time
- Reason For Visit

Store all requests in Google Sheets.

---

## Scenario 2 — Event Registration System

An event organizer wants attendees to register online.

Form Fields:

- Name
- Email
- Company
- Job Title
- Ticket Type

Store registrations in Google Sheets.

---

## Scenario 3 — Job Application Intake

A company wants candidates to submit applications.

Form Fields:

- Name
- Email
- Phone
- Position Applied For
- Years Of Experience

Store applications in Google Sheets.

---

## Scenario 4 — Restaurant Reservation Requests

A restaurant wants customers to request table reservations.

Form Fields:

- Name
- Phone
- Date
- Time
- Number Of Guests

Store requests in Google Sheets.

---

## Scenario 5 — Student Course Registration

An instructor wants students to register for a training course.

Form Fields:

- Student Name
- Email
- Phone
- Course Name

Store registrations in Google Sheets.

---

# Challenge Extension

After completing the project, try adding one of the following:

- Send a confirmation email to the user
- Notify the business owner on Telegram
- Notify the business owner on Slack
- Store the submission in Notion instead of Google Sheets
- Reject duplicate submissions
- Add a submission ID automatically
- Record the submission timestamp