## Project Overview

In this project, you will build a Telegram bot that automatically responds to user messages based on predefined commands and keywords.

Users can interact with the bot through Telegram, and the bot will route requests to different responses depending on what the user sends.

This project introduces conversational workflows and serves as the foundation for more advanced AI-powered bots later in the course.

You will learn:

- Telegram integrations
- Event-driven workflows
- Message routing
- Switch nodes
- User interaction design
- Basic session awareness
- Chatbot fundamentals

This is one of the most requested freelance automation projects, especially for small businesses, educational organizations, communities, and customer support teams.

---

# Client Scenario

## The Client

Hassan runs a training center that teaches programming and technology courses.

Every day, potential students ask the same questions:

- What courses do you offer?
- How much do they cost?
- Where are the classes held?
- How can I register?
- What are your support hours?

His team spends hours answering repetitive questions.

Many inquiries arrive outside working hours, causing delays and missed opportunities.

Hassan wants a Telegram bot that can answer common questions automatically and provide instant information 24/7.

---

# Business Goal

Whenever a user sends a message to the Telegram bot:

1. Receive the message.
2. Determine what the user wants.
3. Send the appropriate response.
4. Provide instant self-service support.
5. Reduce repetitive work for staff.

The goal is to improve response times while reducing manual support workload.

---

# Technical Requirements From The Client

## Supported Commands

The client wants the bot to support:

### /start

Returns:

```text
Welcome to Tech Academy!

How can I help you today?

Available commands:
/courses
/pricing
/location
/contact
```

---

### /courses

Returns:

```text
Available Courses:

- Web Development
- Python Programming
- Data Analysis
- AI Automation
```

---

### /pricing

Returns:

```text
Course pricing starts from $99.

Contact our team for detailed pricing information.
```

---

### /location

Returns:

```text
Our training center is located in Downtown Cairo.

Google Maps:
https://maps.google.com/...
```

---

### /contact

Returns:

```text
Email: info@example.com

Phone: +20 123456789
```

---

## Unknown Messages

If a user sends an unsupported command:

Example:

```text
Can you build websites?
```

The bot should respond:

```text
Sorry, I don't understand that command.

Type /start to see available options.
```

---

## Response Time

The client expects:

- Instant responses
- 24/7 availability

---

## User Experience Requirements

The bot should:

- Be easy to use
- Guide users toward available commands
- Always provide a helpful response

---

## Tools Required

- Telegram Trigger
- Switch Node
- Telegram Send Message Node

Optional:

- Set Node
- Google Sheets
- Airtable

---

# What The Learner Will Practice

By completing this project, you will learn:

### Telegram Integration

Connecting N8N to Telegram.

### Event-Driven Workflows

Building workflows that react to incoming messages.

### Message Routing

Using Switch nodes to direct users to the correct path.

### Bot Design

Creating clear conversational flows.

### User Experience

Designing responses that guide users effectively.

### Basic State Awareness

Understanding how chat systems identify users.

### Customer Support Automation

Replacing repetitive manual communication.

---

# Success Criteria

The project is complete when:

- The Telegram bot receives messages.
- Supported commands return correct responses.
- Unknown messages are handled gracefully.
- Users receive responses instantly.
- No human intervention is required.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Restaurant Information Bot

Customers can ask for:

- Menu
- Location
- Opening hours
- Reservation contact information

Commands:

```text
/menu
/hours
/location
/reserve
```

---

## Scenario 2 — School Information Bot

Students can ask for:

- Class schedules
- Exam dates
- Contact information
- School announcements

Commands:

```text
/schedule
/exams
/contact
/news
```

---

## Scenario 3 — Gym Membership Bot

Members can request:

- Membership plans
- Working hours
- Trainer information
- Contact details

Commands:

```text
/plans
/trainers
/hours
/contact
```

---

## Scenario 4 — Community FAQ Bot

A community manager wants users to access:

- Rules
- Events
- Resources
- Contact information

Commands:

```text
/rules
/events
/resources
/help
```

---

## Scenario 5 — Real Estate Inquiry Bot

Potential buyers can request:

- Available properties
- Contact information
- Office location
- Viewing appointments

Commands:

```text
/properties
/contact
/location
/book
```

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Store user interactions in Google Sheets.
- Add inline keyboard buttons instead of commands.
- Create a multilingual version of the bot.
- Connect the bot to Notion for dynamic content.
- Allow administrators to update responses from a Google Sheet.
- Add voice message support.
- Add image and document responses.
- Build a support ticket system.
- Send notifications to staff when users request human assistance.
- Add AI-generated responses for unknown questions.
- Create user profiles and interaction history.
- Connect the bot to a CRM system.
- Build a lead capture workflow.
- Add appointment booking functionality.
- Upgrade the bot into an AI assistant.

---

# Production Insight

This project introduces one of the most important automation patterns:

**Receive Message → Identify Intent → Route → Respond**

You will see this pattern in:

- Telegram bots
- WhatsApp bots
- Slack assistants
- Customer support systems
- AI chatbots
- Voice assistants
- Internal company help desks

The Simple Telegram Bot is often the first step toward building sophisticated conversational systems. Later projects will add memory, AI, external tools, and retrieval systems, but nearly all chat-based automations still follow this same foundational pattern.