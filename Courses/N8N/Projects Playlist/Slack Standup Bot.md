## Project Overview

In this project, you will build an automated Slack bot that posts a daily standup message to a team channel.

Every morning, the bot will send a structured standup prompt asking team members to share:

- What they worked on yesterday
- What they will work on today
- Any blockers they are facing

This project introduces learners to team communication automations and demonstrates how workflows can automate recurring operational tasks.

You will learn:

- Scheduled automations
- Slack integrations
- Message formatting
- Block Kit basics
- Team communication workflows
- Internal business automation

This is one of the most common automations used inside software companies, startups, agencies, and remote teams.

---

# Client Scenario

## The Client

Omar manages a remote software development team.

The team consists of:

- Developers
- Designers
- QA engineers
- Product managers

Every morning, Omar asks the team to provide a daily standup update.

Currently, the process is manual:

- Omar posts the same message every morning.
- Sometimes he forgets.
- The format changes frequently.
- New team members don't know what information to provide.

As the team grows, Omar wants a consistent and automated standup process.

---

# Business Goal

Every weekday at 9:00 AM:

1. A standup message should be posted automatically.
2. Team members should know exactly how to respond.
3. The format should be consistent every day.
4. Managers should have visibility into team progress and blockers.

The goal is to remove repetitive administrative work and create a predictable communication process.

---

# Technical Requirements From The Client

## Schedule Requirements

The workflow should:

- Run Monday through Friday
- Execute at 9:00 AM
- Skip weekends

---

## Slack Channel

The standup prompt should be posted to:

```text
#daily-standup
```

---

## Message Content

The client wants the following format:

```text
Good morning team ☀️

Please share your daily standup update:

1. What did you accomplish yesterday?
2. What are you working on today?
3. Do you have any blockers?

Please post your update in this thread.
```

---

## Message Formatting

The message should:

- Be visually clean
- Use Slack Block Kit
- Include headings
- Include bullet points
- Encourage replies in a thread

---

## Failure Handling

If Slack is unavailable:

- Log the failure
- Notify the manager via email

---

## Tools Required

- Schedule Trigger
- Slack Node

Optional:

- IF Node
- Gmail Node
- Set Node

---

# What The Learner Will Practice

By completing this project, you will learn:

### Scheduled Workflows

How to run automations automatically at specific times.

### Slack Integration

Connecting N8N with Slack.

### Message Formatting

Building professional messages using Block Kit.

### Internal Automation

Automating team processes instead of customer-facing processes.

### Business Operations

Understanding how automation improves communication workflows.

### Error Handling

Handling failures when external services are unavailable.

---

# Success Criteria

The project is complete when:

- The workflow runs every weekday.
- A standup prompt appears in Slack.
- The message is properly formatted.
- Team members know how to respond.
- No manual intervention is required.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Daily Sales Team Check-In

Every morning, post a message asking sales representatives:

- Deals closed yesterday
- Deals in progress
- Challenges requiring assistance

Post in:

```text
#sales-team
```

---

## Scenario 2 — Customer Support Handoff

Every shift change, post a checklist asking support agents to report:

- Open tickets
- Escalations
- Urgent customer issues

Post in:

```text
#support-team
```

---

## Scenario 3 — Marketing Team Daily Sync

Every morning, ask marketers to provide updates on:

- Campaign performance
- Content published
- Upcoming launches

Post in:

```text
#marketing
```

---

## Scenario 4 — Construction Site Daily Report Reminder

Every morning, remind site supervisors to submit:

- Work completed
- Safety incidents
- Material shortages

Post in:

```text
#site-operations
```

---

## Scenario 5 — School Staff Morning Briefing

Every school day, remind teachers to submit:

- Attendance concerns
- Schedule changes
- Student issues

Post in:

```text
#faculty
```

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Collect responses and save them to Google Sheets.
- Collect responses and save them to Notion.
- Send a reminder to team members who have not responded after 2 hours.
- Generate an AI summary of all standup responses.
- Send the summary to managers at the end of the day.
- Post different standup questions on different days of the week.
- Create separate standups for multiple teams.
- Track response rates over time.
- Build a leaderboard showing participation rates.
- Detect blockers automatically and notify managers.
- Store all standups in a searchable knowledge base.
- Create a dashboard showing team activity trends.
- Send standup prompts to Microsoft Teams instead of Slack.
- Allow team leads to configure standup questions from a Google Sheet.

---

# Production Insight

This project introduces an important automation category:

**Scheduled Internal Operations**

The pattern is:

**Schedule → Notify → Collect Responses → Analyze**

This same pattern is used for:

- Daily standups
- Sales reporting
- Compliance reminders
- Shift handovers
- KPI reporting
- Employee checklists
- Executive summaries

Many companies generate significant operational efficiency simply by automating repetitive communication processes like these.