
## Project Overview

In this project, you will build an automation that sends personalized emails to multiple recipients automatically.

The workflow runs on a schedule, reads recipient information from a Google Sheet, and sends each person a customized email.

This project introduces one of the most important concepts in N8N:

- Scheduled workflows
- Reading data from external systems
- Working with multiple items
- Dynamic expressions
- Personalized communication
- Conditional logic
- Batch processing

This is one of the most common automation requests businesses ask for.

---

# Client Scenario

## The Client

Ahmed runs a training company that offers online technology courses.

Every week, new students enroll in his programs. Before each course starts, Ahmed manually sends reminder emails to every student.

His process currently looks like this:

1. Open a spreadsheet containing student information.
2. Copy each student's email address.
3. Write or paste a reminder email.
4. Personalize the email with the student's name.
5. Repeat for dozens or hundreds of students.

As the company grows, this process consumes hours every week.

Ahmed wants the entire process automated.

---

# Business Goal

Every morning at 9:00 AM, the system should:

1. Check a Google Sheet containing student records.
2. Find students who should receive a reminder email.
3. Generate a personalized message for each student.
4. Send the email automatically.
5. Mark the email as sent.

The goal is to eliminate repetitive manual work while ensuring every student receives their reminder.

---

# Technical Requirements From The Client

## Data Source

The client stores student information inside Google Sheets.

Example columns:

| Column        |
| ------------- |
| Student Name  |
| Email         |
| Course Name   |
| Course Date   |
| Reminder Sent |
|               |

---

## Schedule Requirements

The workflow should:

- Run every day at 9:00 AM
- Automatically check the spreadsheet
- Process all eligible students

---

## Email Requirements

Each email should contain:

- Student name
- Course name
- Course start date

Example:

Hello Sarah,

This is a reminder that your course "Introduction to N8N" starts on June 20.

We look forward to seeing you.

---

## Business Rules

Only send emails when:

- Email address exists
- Reminder Sent = No

After sending:

- Update Reminder Sent = Yes

This prevents duplicate emails.

---

## Error Handling Requirements

If an email address is missing:

- Skip the row
- Do not stop the workflow

If email sending fails:

- Log the failure
- Continue processing other students

---

## Tools Required

- Schedule Trigger
- Google Sheets (Read)
- IF Node
- Gmail Node
- Google Sheets (Update)

Optional:

- Set Node
- Error Workflow

---

# What The Learner Will Practice

By completing this project, you will learn:

### Schedule Triggers

How workflows execute automatically without human interaction.

### Reading External Data

How to retrieve information from Google Sheets.

### Working With Multiple Items

How N8N automatically processes multiple rows.

### Dynamic Expressions

Using spreadsheet values inside email messages.

### Conditional Logic

Using IF nodes to decide who receives emails.

### Updating Existing Records

Writing information back into Google Sheets.

### Idempotency Basics

Preventing duplicate actions from happening twice.

---

# Success Criteria

The project is complete when:

- The workflow runs automatically.
- Student data is read successfully.
- Personalized emails are generated.
- Eligible students receive emails.
- Sent emails are marked in Google Sheets.
- Students never receive duplicate reminders.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Monthly Invoice Reminder System

A freelance accountant wants clients with unpaid invoices to receive reminder emails automatically.

Spreadsheet Columns:

- Client Name
- Email
- Invoice Number
- Due Date
- Reminder Sent

---

## Scenario 2 — Job Interview Reminder System

An HR department wants candidates to receive interview reminders automatically.

Spreadsheet Columns:

- Candidate Name
- Email
- Interview Date
- Interview Time
- Reminder Sent

---

## Scenario 3 — Membership Renewal Reminder

A gym wants members to receive renewal reminders before their subscription expires.

Spreadsheet Columns:

- Member Name
- Email
- Expiration Date
- Reminder Sent

---

## Scenario 4 — Webinar Reminder System

An event organizer wants registered attendees to receive reminders one day before a webinar.

Spreadsheet Columns:

- Name
- Email
- Webinar Name
- Webinar Date
- Reminder Sent

---

## Scenario 5 — Customer Feedback Request System

An e-commerce business wants customers to receive a feedback request email three days after purchase.

Spreadsheet Columns:

- Customer Name
- Email
- Purchase Date
- Feedback Sent

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Send the email as HTML instead of plain text.
- Add the company logo to the email.
- Send a copy of every email to the manager.
- Create a Telegram notification whenever an email is sent.
- Create a Slack notification showing daily email statistics.
- Add a "Last Sent Date" column.
- Stop sending emails after 3 failed attempts.
- Generate the email body using AI.
- Attach a PDF file to each email.
- Allow different email templates based on the course name.
- Send emails only during business hours.
- Generate a daily report showing:
    - Emails sent
    - Emails skipped
    - Emails failed