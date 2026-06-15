## Project Overview

In this project, you will replace a traditional backend server with an N8N workflow.

A website contact form will send data directly to an N8N webhook. The workflow will validate the submitted information, send a confirmation email to the user, notify the business owner, and return a custom response back to the website.

This project introduces one of the most powerful concepts in N8N:

- Webhooks
- API-style workflows
- Input validation
- Authentication
- HTTP responses
- Multi-step processing
- Backend replacement patterns

This is often the first moment learners realize that N8N is not just an automation tool—it can also act as a lightweight backend service.

---

# Client Scenario

## The Client

Mariam owns a digital marketing agency.

Her company website contains a "Contact Us" page where potential customers can submit inquiries.

Currently, when someone submits the form:

- The website sends the information to a custom backend.
- The backend stores the submission.
- The backend sends notifications.

The problem is that every small change requires hiring a developer.

Mariam wants a simpler solution that her team can manage without touching backend code.

She wants N8N to become the backend for the contact form.

---

# Business Goal

Whenever a visitor submits the contact form:

1. The request should be received by N8N.
2. The submitted data should be validated.
3. A confirmation email should be sent to the visitor.
4. A notification email should be sent to the agency owner.
5. The workflow should return a success response to the website.
6. Invalid requests should be rejected with a meaningful error message.

The goal is to automate the entire contact request process without maintaining a custom backend application.

---

# Technical Requirements From The Client

## Contact Form Fields

The form should collect:

- Full Name
- Email Address
- Company Name
- Service Interested In
- Message

---

## Validation Rules

Before processing:

- Name is required
- Email is required
- Email must be valid
- Message is required
- Message must contain at least 10 characters

If validation fails:

- Reject the request
- Return an error response

Example:

```json
{
  "success": false,
  "message": "Email address is required."
}
```

---

## Confirmation Email

The visitor should receive:

- Thank you message
- Confirmation that the inquiry was received
- Expected response timeframe

Example:

"Thank you for contacting us. Our team will review your request and respond within 24 business hours."

---

## Internal Notification Email

The agency owner should receive:

- Customer name
- Email
- Company
- Service requested
- Full message

This allows immediate follow-up.

---

## Webhook Response

If successful:

```json
{
  "success": true,
  "message": "Your request has been received."
}
```

If validation fails:

```json
{
  "success": false,
  "message": "Validation failed."
}
```

---

## Security Requirements

The client wants basic protection against unauthorized requests.

Use:

- Header Authentication

Example:

```http
X-API-Key: my-secret-key
```

Requests without a valid API key should be rejected.

---

## Tools Required

- Webhook Trigger
- IF Node
- Set Node
- Gmail Node
- Respond to Webhook Node

Optional:

- Code Node
- Google Sheets Node
- Error Workflow

---

# What The Learner Will Practice

By completing this project, you will learn:

### Webhooks

How external applications send data into N8N.

### API Fundamentals

How HTTP requests and responses work.

### Request Validation

How to verify incoming data before processing.

### Authentication

How to protect endpoints from unauthorized access.

### Multi-Branch Logic

Different paths for valid and invalid requests.

### Email Automation

Sending multiple emails from a single workflow.

### Custom Responses

Returning structured JSON back to the calling application.

### Backend Thinking

How to design workflows that behave like APIs.

---

# Success Criteria

The project is complete when:

- The webhook receives requests successfully.
- Authentication is enforced.
- Validation works correctly.
- Valid requests send both emails.
- Invalid requests are rejected.
- The website receives a proper JSON response.
- No backend server code is required.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Support Ticket Submission API

A software company wants customers to submit support requests through a website form.

Fields:

- Name
- Email
- Product
- Priority
- Issue Description

Send confirmation to the customer and notification to the support team.

---

## Scenario 2 — Real Estate Property Inquiry Form

A real estate agency wants potential buyers to inquire about properties.

Fields:

- Name
- Email
- Phone
- Property ID
- Message

Notify the assigned agent automatically.

---

## Scenario 3 — Restaurant Catering Request Form

A restaurant wants businesses to submit catering requests online.

Fields:

- Company Name
- Contact Person
- Event Date
- Guest Count
- Requirements

Send confirmation and notify the sales team.

---

## Scenario 4 — Speaker Application Form

A conference organizer wants speakers to apply through a website.

Fields:

- Name
- Email
- Topic Title
- Experience
- Abstract

Store submissions and notify organizers.

---

## Scenario 5 — Service Quote Request API

A home maintenance company wants visitors to request service estimates.

Fields:

- Name
- Email
- Service Type
- Address
- Description

Generate internal notifications for the sales team.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Save all submissions into Google Sheets.
- Save all submissions into Notion.
- Generate a unique ticket number for every request.
- Send a Telegram notification to the business owner.
- Send a Slack notification to the sales team.
- Rate-limit requests from the same IP address.
- Detect spam messages using AI.
- Categorize inquiries automatically using AI.
- Create a CRM record in HubSpot or Airtable.
- Attach uploaded files to the internal notification email.
- Add reCAPTCHA verification.
- Log every API request and response.
- Return different responses based on inquiry type.
- Create a dashboard showing total inquiries received.
- Implement webhook signature verification instead of a simple API key.