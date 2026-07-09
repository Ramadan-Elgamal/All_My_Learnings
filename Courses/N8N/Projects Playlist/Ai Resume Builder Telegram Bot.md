## Project Overview

In this project, you will build an AI-powered Resume Builder that lives entirely inside Telegram.

Instead of asking users to fill out a long form, the bot acts like a professional career coach. It interviews the user one question at a time, remembers previous answers, retrieves inspiration from a library of professional resume templates using Retrieval-Augmented Generation (RAG), and generates a polished ATS-friendly resume.

Finally, the bot exports the resume as a PDF or Word document and sends it back to the user.

This project combines conversational AI, memory, RAG, document generation, and Telegram automation into a production-style workflow.

---

# Client Scenario

## The Client

CareerLaunch is a career coaching startup that helps recent graduates and job seekers create professional resumes.

Their current process is entirely manual:

1. Clients complete a lengthy Google Form.
2. A career coach reviews the information.
3. The coach rewrites the resume.
4. A designer formats it.
5. The PDF is emailed back.

This process takes several hours per client.

CareerLaunch wants to automate most of the process while still providing resumes that look professionally written and well-structured.

Instead of filling out forms, users should simply chat with a Telegram bot.

---

# Business Goal

The client wants a Telegram bot that can:

1. Interview the user naturally.
2. Collect all resume information.
3. Remember previous answers.
4. Ask follow-up questions when information is missing.
5. Retrieve similar professional resume templates.
6. Generate an ATS-friendly resume.
7. Export it as PDF or DOCX.
8. Send the finished resume back through Telegram.

---

# Technical Requirements From The Client

## Telegram Bot

The entire experience must happen inside Telegram.

The bot should support commands such as:

- `/start`
- `/newcv`
- `/status`
- `/edit`
- `/generate`
- `/review`
- `/templates`
- `/help`

The bot should rely primarily on conversation and inline buttons instead of requiring users to memorize commands.

---

## Conversational Resume Interview

The AI should guide users through the following sections:

- Basic Information
- Professional Summary
- Work Experience
- Education
- Skills
- Projects
- Certificates
- Languages
- Interests

The AI should ask only one question at a time.

Example:

> What is your full name?

↓

> What's your email address?

↓

> Do you have a LinkedIn profile?

↓

> Great! Let's move on to your professional summary.

---

## Progress Tracking

The bot should track the user's progress.

Example:

```text
Resume Progress

✅ Basic Information

✅ Professional Summary

⬜ Work Experience

⬜ Education

⬜ Skills

⬜ Projects

⬜ Certificates

⬜ Languages

⬜ Interests
```

The `/status` command should display the current completion status.

---

## Conversation Memory

Each Telegram user should have an independent conversation history.

The AI must:

- Remember previous answers.
- Never ask for information already collected.
- Resume unfinished sessions automatically.

---

## Resume Data Storage

Store collected information in a structured format.

Example fields:

|Field|Description|
|---|---|
|Name|Full name|
|Contact|Email, phone, LinkedIn|
|Summary|Professional profile|
|Experience|Previous jobs|
|Education|Degrees|
|Skills|Technical & soft skills|
|Projects|Personal & professional|
|Certificates|Certifications|
|Languages|Spoken languages|
|Interests|Optional section|

Storage options may include:

- Google Sheets
- Airtable
- PostgreSQL
- N8N Data Store

---

## Resume Template Library (RAG)

Create a knowledge base containing high-quality resume examples.

Examples:

- Software Engineer Resume
- Frontend Developer Resume
- Backend Developer Resume
- Data Scientist Resume
- DevOps Engineer Resume
- UI/UX Designer Resume
- Marketing Specialist Resume

When generating a resume, retrieve the most relevant examples to guide formatting, wording, and section organization.

---

## Resume Generation

Once all required information has been collected, generate a complete resume using:

- User information
- Retrieved templates
- ATS best practices

The AI should improve grammar, wording, and formatting while preserving factual accuracy.

---

## Resume Review

The client wants every generated resume reviewed before export.

The reviewer should evaluate:

- Grammar
- Formatting
- Missing information
- ATS compatibility
- Action verbs
- Measurable achievements
- Professional tone

Provide a score from 0–100.

If the score is below the target threshold, improve the resume automatically before exporting.

---

## Export Options

Generate resumes in:

- PDF
- DOCX (optional)
- Markdown (optional)

The exported file should maintain professional formatting.

---

## Delivery

When generation is complete:

1. Upload the document.
2. Send it back through Telegram.
3. Notify the user that the resume is ready.

---

## Edit Existing Resume

Users should be able to edit individual sections.

Example:

```
/edit
```

Bot:

> Which section would you like to edit?

- Basic Information
- Work Experience
- Skills
- Projects
- Education
- ...

After editing, regenerate the resume.

---

## Multiple Resume Templates

Allow users to choose different resume styles.

Examples:

- Modern
- Minimal
- Corporate
- Creative
- ATS-Friendly

The selected template influences formatting but not the underlying data.

---

## Security Requirements

The client requires:

- Secure storage of personal information.
- Protected AI API credentials.
- Private conversations.
- No data sharing between users.
- Ability to delete a user's resume data upon request.

---

## Tools Required

Core Nodes:

- Telegram Trigger
- AI Agent
- Window Buffer Memory
- Vector Store
- Embeddings
- Document Loader
- Text Splitter
- HTTP Request
- Code Node
- IF Node
- Set Node

Optional:

- Google Sheets
- PostgreSQL
- Airtable
- HTML to PDF API
- Google Drive

---

# What The Learner Will Practice

By completing this project, you will learn:

### Conversational AI

Building an AI interviewer that collects structured information naturally.

### AI Memory

Maintaining separate conversations for multiple users.

### Retrieval-Augmented Generation (RAG)

Using resume templates to improve generated resumes.

### Prompt Engineering

Designing prompts for interviewing, writing, and reviewing resumes.

### Document Generation

Creating professional resumes from structured data.

### Telegram Automation

Building a conversational chatbot with commands and inline interactions.

### Human-Centered AI

Designing AI experiences that feel natural instead of form-based.

---

# Success Criteria

The project is complete when:

- Users can start a new resume.
- The AI interviews the user naturally.
- Progress is tracked across sections.
- Conversation state is remembered.
- Resume templates are retrieved using RAG.
- A professional resume is generated.
- The resume is reviewed automatically.
- The final document is exported as a PDF.
- The PDF is delivered through Telegram.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — AI Cover Letter Builder

Interview users about a job and generate a personalized cover letter.

---

## Scenario 2 — LinkedIn Profile Optimizer

Analyze a user's experience and generate an optimized LinkedIn profile.

---

## Scenario 3 — AI Portfolio Builder

Collect project information and generate a developer portfolio website.

---

## Scenario 4 — University Application Assistant

Help students prepare application documents, personal statements, and resumes.

---

## Scenario 5 — Freelancer Proposal Generator

Interview freelancers about a project and generate a professional proposal with pricing and timeline.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Job Description Analyzer that tailors the resume to a specific vacancy.
- ATS Keyword Optimizer that suggests missing keywords.
- Cover Letter Generator based on the generated resume.
- LinkedIn profile generation.
- Voice message support using speech-to-text.
- Multiple language resume generation.
- Resume version history.
- Multiple resume variants for different industries.
- AI Career Advisor that suggests skills to learn.
- AI Mock Interview that asks interview questions based on the generated resume.
- Automatic publishing to Google Drive or Notion.
- One-click resume sharing via a secure public link.

---

# Production Insight

This project demonstrates a modern AI application architecture where conversational AI, memory, retrieval, and document generation work together to deliver a complete end-user product.

Rather than acting as a simple chatbot, the AI becomes a career assistant that interviews users, gathers structured information, retrieves relevant examples from a knowledge base, produces a professional resume, evaluates its own work, and delivers a polished document.

The same architecture can be adapted to build AI-powered assistants for legal documents, business proposals, grant applications, insurance claims, onboarding questionnaires, and many other document-centric workflows, making it an excellent capstone project for learning advanced AI automation with N8N.