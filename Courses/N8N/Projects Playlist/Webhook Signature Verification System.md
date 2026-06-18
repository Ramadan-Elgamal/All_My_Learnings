## Project Overview

In this project, you will build a secure webhook handler that verifies incoming requests before processing them.

Many SaaS platforms send data to your systems using webhooks:

- GitHub
- Stripe
- Shopify
- Slack
- Meta
- Twilio
- Notion

Most beginners focus on processing the data and completely ignore security.

This creates a major problem:

Anyone who discovers the webhook URL can potentially send fake requests.

For example:

```http
POST /webhook/order-created
```

An attacker could send:

```json
{
  "order_id": "12345",
  "amount": 1000000
}
```

Your automation may process it as a legitimate order.

The solution is webhook signature verification.

Before processing any request, the system must verify:

1. Who sent it.
2. Whether the payload was modified.
3. Whether the request is fresh.
4. Whether it is a replay of an old request.

This project teaches one of the most important security concepts in automation:

**Never trust incoming webhook requests.**

---

# Client Scenario

## The Client

Omar runs a small e-commerce company.

His online store uses:

- Shopify
- Stripe
- Shipping provider APIs

When a customer places an order:

1. Shopify sends a webhook.
2. N8N processes the order.
3. Inventory updates.
4. Shipping requests are created.
5. Notifications are sent.

Recently, Omar learned that anyone with the webhook URL could potentially send fake requests.

If a fake order is processed:

- Inventory could be modified.
- Customers could receive incorrect emails.
- Reports could become inaccurate.
- Financial records could be affected.

Omar wants every incoming webhook request verified before it reaches business logic.

---

# Business Goal

When a webhook request arrives:

1. Verify the request signature.
2. Verify the request timestamp.
3. Detect replay attacks.
4. Reject invalid requests.
5. Process only trusted requests.

The goal is to ensure that only legitimate systems can trigger the automation.

---

# Technical Requirements From The Client

## Incoming Webhook

Example endpoint:

```http
POST /webhook/order-created
```

---

## Secret Key

A shared secret should exist between:

```text
External Service
```

and

```text
N8N
```

Example:

```text
super-secret-key
```

The secret must never be exposed publicly.

---

## Signature Header

Incoming requests contain:

```http
X-Signature
```

Example:

```text
9f3d7c2a4b...
```

The workflow must read this header.

---

## Request Verification

The workflow must:

1. Read the raw request body.
2. Compute its own signature.
3. Compare it to the received signature.

If both match:

```text
Request Trusted
```

Otherwise:

```text
Reject Request
```

---

## HMAC-SHA256 Verification

The client requires:

```text
HMAC-SHA256
```

verification.

Example concept:

```text
Signature =
HMAC_SHA256(
  SecretKey,
  RawRequestBody
)
```

The workflow must generate the expected hash and compare it.

---

## Tampering Detection

If someone modifies the payload:

Original:

```json
{
  "amount": 100
}
```

Modified:

```json
{
  "amount": 100000
}
```

The signature should no longer match.

The request must be rejected.

---

## Timestamp Validation

Incoming requests include:

```http
X-Timestamp
```

Example:

```text
2026-06-15T10:00:00Z
```

The workflow should verify freshness.

Allowed window:

```text
5 Minutes
```

If the timestamp is older:

```http
401 Unauthorized
```

---

## Replay Attack Prevention

An attacker may capture a legitimate request and resend it later.

Example:

```text
Valid request from yesterday
```

Without protection, the system may process it again.

The workflow should:

1. Validate timestamp.
2. Track processed request IDs.

Duplicate requests should be rejected.

---

## Request ID Tracking

Incoming requests contain:

```http
X-Request-ID
```

Example:

```text
req_12345
```

Store processed IDs in:

- Data Store
- Redis
- Database
- Google Sheets

If an ID already exists:

```http
409 Conflict
```

or

```http
401 Unauthorized
```

---

## Response Handling

### Successful Verification

Return:

```json
{
  "status": "accepted"
}
```

Status code:

```http
200 OK
```

---

### Invalid Signature

Return:

```json
{
  "error": "invalid signature"
}
```

Status code:

```http
401 Unauthorized
```

---

### Expired Timestamp

Return:

```json
{
  "error": "request expired"
}
```

Status code:

```http
401 Unauthorized
```

---

### Replay Attack

Return:

```json
{
  "error": "duplicate request"
}
```

Status code:

```http
409 Conflict
```

---

## Audit Logging

Track:

|Field|Description|
|---|---|
|Timestamp|Request time|
|Request ID|Unique request|
|Source System|Sender|
|Verification Result|Pass / Fail|
|Failure Reason|Invalid signature, replay, expired timestamp|

Store logs in:

- Google Sheets
- Airtable
- PostgreSQL

---

## Security Alerts

Notify administrators when:

### Multiple Failed Signatures

Example:

```text
10 Invalid Requests Within 5 Minutes
```

Possible attack attempt.

---

### Replay Attempts

Example:

```text
Same Request ID Received Multiple Times
```

---

### Suspicious Sources

Example:

```text
Unknown IP Address
```

---

## Monitoring Dashboard

Track:

|Metric|Description|
|---|---|
|Verified Requests|Accepted|
|Rejected Requests|Failed|
|Replay Attempts|Security incidents|
|Invalid Signatures|Tampering attempts|
|Expired Requests|Outdated requests|

---

## Security Requirements

The client requires:

- Secret key storage in credentials or environment variables.
- No hardcoded secrets in workflows.
- Full audit trail.
- Replay protection.
- Tamper detection.

---

## Tools Required

Core Nodes:

- Webhook
- Code Node
- IF Node
- Respond to Webhook

Optional:

- Redis
- Data Store
- PostgreSQL
- Slack
- Google Sheets

---

# What The Learner Will Practice

By completing this project, you will learn:

### Webhook Security

Protecting webhook endpoints.

### HMAC Verification

Validating request signatures.

### Authentication Concepts

Verifying trusted senders.

### Replay Attack Prevention

Preventing duplicate processing.

### Audit Logging

Tracking security events.

### Secure Automation Design

Building production-grade workflows.

### Defensive Engineering

Validating all incoming data.

---

# Success Criteria

The project is complete when:

- Incoming signatures are verified.
- Invalid requests are rejected.
- Timestamp validation works.
- Replay attacks are blocked.
- Request IDs are tracked.
- Security logs are generated.
- Alerts are triggered for suspicious activity.
- Only trusted requests reach business logic.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Stripe Payment Webhook Verification

Verify payment events before updating order status.

---

## Scenario 2 — GitHub Webhook Security Gateway

Verify repository events before triggering CI/CD workflows.

---

## Scenario 3 — Shopify Order Verification System

Validate incoming order webhooks before inventory updates.

---

## Scenario 4 — Slack Event Verification Service

Verify Slack event signatures before processing commands.

---

## Scenario 5 — Internal Microservice Security Layer

Protect communication between internal services using signed requests.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Support multiple signing algorithms.
- Key rotation system.
- IP allowlist verification.
- Rate limiting.
- API gateway integration.
- Security incident dashboard.
- Automated threat scoring.
- Geo-location analysis of requests.
- Centralized webhook security service.
- Multi-tenant signature verification.
- Certificate-based verification.
- Zero-trust webhook architecture.
- Security analytics reporting.
- SIEM integration.
- Enterprise webhook firewall.

---

# Production Insight

This project introduces a core security architecture pattern:

**Receive → Verify → Validate → Process**

You will encounter similar implementations in:

- Banking systems
- Financial APIs
- Enterprise integrations

One of the most dangerous mistakes in automation is assuming that a request is trustworthy simply because it reached your webhook URL. In production systems, every incoming request is treated as potentially malicious until proven otherwise. Signature verification ensures the request came from a trusted source, timestamp validation prevents old requests from being reused, and replay protection stops attackers from triggering the same action repeatedly. Together, these controls form the foundation of secure webhook processing.