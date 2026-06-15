## Project Overview

In this project, you will build an automated content aggregation system that collects articles from multiple RSS feeds, filters relevant content, and sends a daily email digest.

Instead of manually visiting dozens of websites every day, the user receives a curated summary directly in their inbox.

You will learn:

- RSS feeds
- Content aggregation
- Working with multiple data sources
- Filtering and deduplication
- HTML email generation
- Daily digest workflows
- Content curation automation

This is one of the most practical automations for content creators, marketers, researchers, founders, investors, and industry professionals.

---

# Client Scenario

## The Client

Nour runs a weekly AI and technology newsletter.

Every morning she spends nearly two hours:

- Visiting AI news websites
- Checking blogs
- Reading product announcements
- Looking through research publications

She then manually collects interesting articles for her newsletter.

The process is repetitive and time-consuming.

Nour wants an automated system that gathers articles from her favorite sources and sends her a single email digest every morning.

This allows her to focus on selecting and writing about the most important stories instead of hunting for them.

---

# Business Goal

Every day at 7:00 AM:

1. Collect articles from multiple RSS feeds.
2. Filter for relevant topics.
3. Remove duplicates.
4. Build a clean email digest.
5. Send the digest to Nour.

The goal is to create a personal news assistant that automatically monitors industry sources.

---

# Technical Requirements From The Client

## RSS Sources

Monitor the following sources:

- OpenAI Blog
- Anthropic Blog
- Google AI Blog
- TechCrunch AI
- Hacker News
- Any additional AI-related RSS feeds

The client should be able to add more feeds later.

---

## Content Filtering

Only include articles related to:

- AI
- Machine Learning
- Automation
- Agents
- LLMs
- Startups

Exclude unrelated content.

---

## Duplicate Prevention

If the same article appears:

- In multiple feeds
- On consecutive days

It should only appear once.

---

## Email Digest Format

The email should contain:

```text
Daily AI Digest

1. Article Title
   Source: TechCrunch
   Link: https://...
   Summary: ...

2. Article Title
   Source: OpenAI
   Link: https://...
   Summary: ...
```

The email should be:

- Easy to scan
- Mobile-friendly
- Professionally formatted

---

## Schedule Requirements

The workflow should:

- Run daily
- Execute at 7:00 AM
- Deliver the digest before work begins

---

## Failure Handling

If one RSS feed fails:

- Continue processing other feeds
- Include available content

The workflow should not fail completely because of a single source.

---

## Tools Required

- Schedule Trigger
- RSS Feed Read Node
- Merge Node
- IF Node
- Gmail Node

Optional:

- Google Sheets
- Set Node
- Code Node

---

# What The Learner Will Practice

By completing this project, you will learn:

### RSS Feeds

How RSS works and why it remains useful.

### Multi-Source Aggregation

Combining data from several sources.

### Content Filtering

Selecting only relevant information.

### Data Deduplication

Preventing duplicate content from appearing.

### HTML Email Generation

Creating professional email digests.

### Workflow Resilience

Handling partial failures gracefully.

### Information Automation

Building systems that collect and organize knowledge automatically.

---

# Success Criteria

The project is complete when:

- RSS feeds are retrieved successfully.
- Relevant articles are filtered.
- Duplicate articles are removed.
- A digest email is generated.
- The email is delivered automatically.
- The workflow continues working even if a feed becomes unavailable.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Cybersecurity Threat Digest

A security analyst wants a daily digest of:

- Security advisories
- Vulnerability reports
- Threat intelligence articles

Sources:

- CISA
- Krebs on Security
- SecurityWeek

---

## Scenario 2 — Startup Funding Tracker

An investor wants a daily report of:

- Startup funding announcements
- Acquisitions
- Venture capital news

Sources:

- TechCrunch
- Crunchbase News
- VentureBeat

---

## Scenario 3 — Developer Learning Digest

A software engineer wants a digest of:

- Programming tutorials
- Open-source releases
- Framework updates

Sources:

- GitHub Blog
- Dev.to
- Smashing Magazine

---

## Scenario 4 — E-Commerce Industry News

An agency serving e-commerce clients wants updates about:

- Shopify
- Amazon Marketplace
- E-commerce trends

Sources:

- Shopify Blog
- EcommerceBytes
- Retail Dive

---

## Scenario 5 — Academic Research Monitor

A university researcher wants updates on newly published papers.

Sources:

- arXiv
- Research blogs
- Academic journals

Filter by selected keywords.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Generate AI summaries for each article.
- Categorize articles automatically using AI.
- Rank articles by importance.
- Send the digest to multiple subscribers.
- Allow subscribers to choose their own topics.
- Store all articles in Notion.
- Store all articles in Airtable.
- Save articles to Raindrop automatically.
- Create a Telegram version of the digest.
- Create a Slack version of the digest.
- Generate a weekly digest in addition to the daily digest.
- Detect trending topics across multiple feeds.
- Translate articles into another language.
- Create an AI-generated executive summary at the top of the email.
- Build a searchable knowledge base from collected articles.

---

# Production Insight

This project introduces a powerful automation pattern:

**Collect → Filter → Deduplicate → Format → Deliver**

You will see this same pattern repeatedly in production systems such as:

- Newsletter platforms
- Market intelligence systems
- Competitive monitoring tools
- Research assistants
- Media monitoring systems
- AI news aggregators
- Executive reporting dashboards

Many successful automation businesses are built entirely around collecting information from multiple sources and transforming it into something more valuable for the end user.