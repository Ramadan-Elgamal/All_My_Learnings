## Project Overview

In this project, you will build a unified API endpoint that collects data from multiple external APIs, combines the results into a single response, and returns it to the client.

This is one of the most common backend patterns used in modern applications.

Instead of forcing applications to call:

- API A
- API B
- API C

individually, an API Aggregator acts as a middle layer:

```text
Client
   ↓
Aggregator API
   ↓
API A
API B
API C
```

The client makes one request and receives one clean response.

This pattern is heavily used in:

- Mobile applications
- SaaS products
- Dashboards
- Internal company portals
- Microservice architectures

The goal of this project is to build a production-ready aggregation service that fetches data from multiple sources, merges it into a standardized format, and handles failures gracefully.

---

# Client Scenario

## The Client

Youssef owns a small e-commerce analytics company.

His customers currently use several different platforms:

- Shopify
- Google Analytics
- Facebook Ads

To view business performance, users must log into each platform separately.

Customers are frustrated because:

- Sales data is in Shopify.
- Traffic data is in Google Analytics.
- Advertising data is in Facebook Ads.

There is no single dashboard showing all metrics together.

Youssef wants a single API endpoint that provides a unified business summary.

---

# Business Goal

When a dashboard requests data:

1. Fetch sales data from Shopify.
2. Fetch traffic data from Google Analytics.
3. Fetch ad performance from Facebook Ads.
4. Combine everything.
5. Return one clean JSON response.

The dashboard should never communicate directly with the individual services.

---

# Technical Requirements From The Client

## API Endpoint

Create a webhook endpoint:

```text
GET /dashboard-summary
```

The endpoint acts as the aggregator.

---

## External APIs

### API 1 — Shopify

Retrieve:

```json
{
  "orders": 152,
  "revenue": 12450
}
```

---

### API 2 — Google Analytics

Retrieve:

```json
{
  "visitors": 8900,
  "bounce_rate": 42
}
```

---

### API 3 — Facebook Ads

Retrieve:

```json
{
  "spend": 1200,
  "clicks": 3400
}
```

---

## Parallel Execution

The client wants all APIs called simultaneously.

Do NOT do:

```text
Call API A
Wait
Call API B
Wait
Call API C
```

Instead:

```text
Call API A
Call API B
Call API C
```

at the same time.

Use parallel branches in N8N.

---

## Response Format

The dashboard should receive:

```json
{
  "sales": {
    "orders": 152,
    "revenue": 12450
  },
  "traffic": {
    "visitors": 8900,
    "bounce_rate": 42
  },
  "advertising": {
    "spend": 1200,
    "clicks": 3400
  }
}
```

---

## Data Normalization

Different APIs may use different naming conventions.

Example:

### API A

```json
{
  "totalRevenue": 12450
}
```

### API B

```json
{
  "revenue_amount": 12450
}
```

Both should become:

```json
{
  "revenue": 12450
}
```

The client wants a consistent schema regardless of source differences.

---

## Timeout Handling

If one API takes too long:

Example:

```text
Facebook Ads API timeout
```

The system should not fail entirely.

Options:

### Option 1

Return partial results:

```json
{
  "sales": {...},
  "traffic": {...},
  "advertising": null
}
```

---

### Option 2

Return an error object:

```json
{
  "advertising_error": "Timeout"
}
```

---

## Failure Handling

If one API is unavailable:

Example:

```text
HTTP 503
```

The workflow should:

1. Retry.
2. Log the failure.
3. Return available data.

The client does not want one API failure to break the entire response.

---

## Authentication

The aggregator endpoint should require:

### Option 1

```text
API Key
```

or

### Option 2

```text
Bearer Token
```

Unauthorized requests should receive:

```http
401 Unauthorized
```

---

## Request Parameters

Support optional filters.

Example:

```http
GET /dashboard-summary?start=2026-01-01&end=2026-01-31
```

The workflow should pass the date range to all relevant APIs.

---

## Audit Logging

Track:

|Field|Description|
|---|---|
|Request ID|Unique request|
|Timestamp|Request time|
|API Calls|Total APIs contacted|
|Duration|Response time|
|Failures|Failed APIs|

Store logs in:

```text
Google Sheets
```

or

```text
Database
```

---

## Monitoring Dashboard

Track:

|Metric|Description|
|---|---|
|Requests Served|Total|
|Average Response Time|Performance|
|API Failures|Reliability|
|Timeout Count|Slow services|
|Success Rate|Availability|

---

## Caching

The client wants to reduce API costs.

If the same request arrives within:

```text
5 Minutes
```

return cached data instead of calling all APIs again.

Possible storage:

- Data Store
- Redis
- Database

---

## Security

The client requires:

- API authentication
- Request logging
- Rate limiting
- Secret management for API credentials

---

## Tools Required

Core Nodes:

- Webhook
- HTTP Request
- Merge
- IF
- Code
- Respond to Webhook

Optional:

- Redis
- Data Store
- PostgreSQL
- Google Sheets

---

# What The Learner Will Practice

By completing this project, you will learn:

### API Integration

Connecting multiple external services.

### Parallel Processing

Running API calls simultaneously.

### Data Normalization

Standardizing inconsistent responses.

### Aggregation Patterns

Combining multiple datasets.

### Error Handling

Managing failures gracefully.

### Caching

Reducing API usage and improving speed.

### Backend Architecture

Building middleware services.

---

# Success Criteria

The project is complete when:

- Multiple APIs are queried.
- Requests run in parallel.
- Responses are normalized.
- Results are merged correctly.
- Authentication works.
- Failures are handled gracefully.
- Logs are generated.
- Cached responses work correctly.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Travel Search Aggregator

Combine flight, hotel, and car rental APIs into one travel search endpoint.

---

## Scenario 2 — Cryptocurrency Market Dashboard

Aggregate prices from multiple exchanges and return a unified market view.

---

## Scenario 3 — Sports Statistics API

Combine player stats, team stats, and live match data into one endpoint.

---

## Scenario 4 — Real Estate Listing Aggregator

Collect property listings from multiple real-estate platforms and return a unified catalog.

---

## Scenario 5 — Job Search Aggregator

Merge job postings from multiple job boards into a single searchable API.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Dynamic API selection.
- User-specific caching.
- GraphQL-style aggregation.
- Request batching.
- Circuit breaker pattern.
- API health monitoring.
- Cost-aware API routing.
- Response compression.
- Distributed caching.
- Multi-region aggregation.
- Streaming partial responses.
- AI-generated summaries of aggregated data.
- Multi-tenant API aggregation.
- Service discovery.
- Full API gateway architecture.

---

# Production Insight

This project introduces a common microservices and backend pattern:

**Client → Aggregator → Multiple Services → Unified Response**

You will find this architecture in:

- Mobile backends
- API gateways
- Enterprise integration platforms
- SaaS dashboards
- Microservice ecosystems
- Data platforms
- Business intelligence tools

A common mistake is exposing every external service directly to the frontend. Professional systems often place an aggregation layer in between. This reduces frontend complexity, improves performance through parallel execution, centralizes authentication and caching, and allows developers to change underlying services without affecting clients. The aggregator becomes the single source of truth for how data is presented to consumers.