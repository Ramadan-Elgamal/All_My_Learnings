## Project Overview

In this project, you will build a complete email drip campaign system that automatically nurtures subscribers through a series of timed emails.

Instead of sending a single email when someone subscribes, the system will guide them through a predefined journey over days or weeks. Each subscriber progresses through the sequence independently based on when they joined.

This project introduces one of the most common marketing automation systems used by businesses, SaaS companies, coaches, agencies, content creators, and e-commerce stores.

Key concepts include:

- State Management
- Scheduled Processing
- Customer Journey Automation
- Email Marketing Automation
- Subscriber Tracking
- Idempotency
- Workflow Separation

This is the type of automation clients frequently request because it directly impacts lead conversion and revenue.

---

# Client Scenario

## The Client

Mona runs an online programming academy.

Visitors can download a free guide called:

```text
"Learn JavaScript in 30 Days"
```

When someone downloads the guide, they are added to a mailing list.

Currently, every subscriber receives only a welcome email.

Mona wants a system that gradually educates subscribers, builds trust, and eventually promotes her paid courses.

She wants the process to happen automatically without manually sending emails.

---

# Business Goal

When a new subscriber joins:

1. Add them to the campaign.
2. Track their progress.
3. Send the correct email at the correct time.
4. Prevent duplicate emails.
5. Stop sending emails if they unsubscribe.

The goal is to nurture leads and increase conversions automatically.

---

# Technical Requirements From The Client

## Subscriber Enrollment

New subscribers arrive through:

```text
N8N Form
```

or

```text
Webhook
```

or

```text
Landing Page Integration
```

Collected fields:

|Field|Description|
|---|---|
|Subscriber ID|Unique identifier|
|Name|Subscriber name|
|Email|Email address|
|Signup Date|Enrollment date|
|Campaign Status|Active / Unsubscribed|

---

## Subscriber Database

Store subscribers in:

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
|Subscriber ID|Unique ID|
|Email|Email address|
|Current Step|Current email stage|
|Last Email Sent|Timestamp|
|Next Email Due|Timestamp|
|Status|Active / Completed / Unsubscribed|

---

## Email Sequence

### Day 0 — Welcome Email

Subject:

```text
Welcome to the JavaScript Learning Journey
```

Content:

- Deliver free guide.
- Introduce the academy.
- Set expectations.

---

### Day 3 — Educational Email

Subject:

```text
The Biggest Mistakes Beginners Make
```

Content:

- Helpful learning tips.
- Common pitfalls.
- Additional resources.

---

### Day 7 — Value Email

Subject:

```text
How Our Students Build Real Projects
```

Content:

- Success stories.
- Case studies.
- Project examples.

---

### Day 10 — Promotional Email

Subject:

```text
Ready to Go Further?
```

Content:

- Paid course offer.
- Limited-time discount.
- Call to action.

---

## Campaign Processor

Create a separate workflow that runs periodically.

Example:

```text
Every Hour
```

Responsibilities:

1. Find subscribers whose next email is due.
2. Determine which step they are currently on.
3. Send the correct email.
4. Update subscriber status.
5. Schedule the next step.

---

## Unsubscribe Handling

Every email must include:

```text
Unsubscribe Link
```

When clicked:

- Mark subscriber as unsubscribed.
- Stop future emails.
- Record unsubscribe date.

---

## Duplicate Prevention

The client requires:

```text
Never send the same email twice.
```

Even if:

- The workflow runs twice.
- N8N restarts.
- A retry occurs.

Track email history before sending.

---

## Email Logging

Store email activity:

|Field|Description|
|---|---|
|Subscriber ID|Subscriber|
|Email Step|Sent stage|
|Sent At|Timestamp|
|Status|Success / Failed|

---

## Failure Handling

If email delivery fails:

### Temporary Failure

- Retry later.

Examples:

- Network issues
- Provider timeout

---

### Permanent Failure

Examples:

- Invalid email
- Hard bounce

Actions:

- Mark subscriber as invalid.
- Notify administrator.

---

## Reporting

Generate weekly statistics:

|Metric|Description|
|---|---|
|New Subscribers|New signups|
|Emails Sent|Total delivered|
|Unsubscribes|Opt-outs|
|Campaign Completion Rate|Reached final step|
|Conversion Rate|Purchased course|

Deliver reports via:

```text
Email
```

or

```text
Slack
```

---

## Tools Required

Core Nodes:

- Form Trigger
- Webhook
- Schedule Trigger
- Gmail
- Google Sheets
- Airtable
- IF Node

Optional:

- Slack
- Notion
- CRM Systems

---

# What The Learner Will Practice

By completing this project, you will learn:

### State-Based Workflows

Tracking where each user is in a process.

### Scheduled Automation

Running workflows based on time.

### Customer Journey Design

Creating automated user experiences.

### Idempotency

Preventing duplicate actions.

### Email Marketing Automation

Building real campaign systems.

### Subscriber Lifecycle Management

Managing enrollments and exits.

### Workflow Separation

Separating enrollment logic from campaign execution logic.

---

# Success Criteria

The project is complete when:

- Subscribers can enroll successfully.
- Emails are sent at the correct times.
- Progress is tracked correctly.
- Duplicate emails are prevented.
- Unsubscribes stop future emails.
- Reports are generated.
- Failed deliveries are handled gracefully.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — SaaS Product Onboarding Sequence

Teach new users how to use a software product through a series of onboarding emails.

---

## Scenario 2 — E-Commerce Abandoned Cart Recovery

Send follow-up emails to customers who left products in their cart.

---

## Scenario 3 — Real Estate Lead Nurturing

Educate potential buyers about available properties and financing options.

---

## Scenario 4 — Fitness Coaching Program

Guide new clients through a 30-day fitness journey.

---

## Scenario 5 — Newsletter Subscriber Warm-Up Sequence

Introduce new subscribers to your content and best-performing articles.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Multiple campaigns.
- Campaign branching based on user actions.
- Lead scoring.
- Dynamic content personalization.
- A/B testing.
- Timezone-aware sending.
- SMS follow-up messages.
- WhatsApp campaign integration.
- AI-generated email content.
- CRM synchronization.
- Engagement tracking.
- Open and click analytics.
- Campaign performance dashboards.
- Multi-language campaigns.
- Visual campaign builder.

---

# Production Insight

This project introduces a common marketing automation pattern:

**Enroll → Track State → Wait → Send → Update State → Repeat**

You will encounter similar systems in:

- SaaS companies
- Online academies
- Marketing agencies
- E-commerce stores
- Coaching businesses
- Newsletters
- Enterprise CRM platforms

One of the most important lessons from this project is that marketing automation is fundamentally a state-management problem. The difficult part is not sending emails—it is reliably tracking where every subscriber is in their journey and ensuring they receive the right message at the right time exactly once. Mastering this pattern prepares you for many other workflow types that depend on long-running processes and user progression through multiple stages.