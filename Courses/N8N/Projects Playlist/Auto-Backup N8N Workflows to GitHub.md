## Project Overview

In this project, you will build a workflow that automatically backs up all N8N workflows to a GitHub repository.

The automation will run on a schedule, retrieve workflow definitions using the N8N API, convert them into JSON files, and commit them to GitHub.

This is your first "meta-workflow"—a workflow that manages and protects other workflows.

You will learn:

- Working with the N8N API
- GitHub integration
- File creation and management
- Scheduled backups
- Version control concepts
- Disaster recovery planning
- Production best practices

This project teaches an important lesson: professional automations are not complete unless they can be recovered when something goes wrong.

---

# Client Scenario

## The Client

Youssef owns a small automation agency.

His team has built dozens of workflows for clients:

- Lead capture systems
- CRM automations
- Email campaigns
- AI agents
- Internal business tools

Everything runs inside a self-hosted N8N instance.

One day, a server update goes wrong.

Several workflows are accidentally deleted.

The team has no recent backup.

Hours of work are lost.

After recovering from the incident, Youssef decides that every workflow should be backed up automatically and versioned properly.

He wants every workflow stored in GitHub so that:

- Changes can be tracked.
- Previous versions can be restored.
- Accidental deletions are recoverable.
- Team members can review workflow changes.

---

# Business Goal

Every night:

1. Retrieve all workflows from N8N.
2. Export each workflow as JSON.
3. Save the files to GitHub.
4. Create a commit containing any changes.
5. Maintain a complete version history.

The goal is to ensure the business never loses workflow definitions again.

---

# Technical Requirements From The Client

## Schedule Requirements

The backup should run:

- Every day at 2:00 AM
- Automatically
- Without manual intervention

---

## Workflows To Backup

The client wants:

- All active workflows
- All inactive workflows

Nothing should be excluded.

---

## File Structure

The GitHub repository should contain:

```text
/workflows
    Lead Capture.json
    Support Bot.json
    Customer Onboarding.json
    Weekly Report.json
```

Each workflow should have its own JSON file.

---

## Version Control Requirements

The system should:

- Create commits only when changes exist
- Preserve history
- Allow rollback to previous versions

Example commit message:

```text
Backup N8N Workflows - 2026-06-15
```

---

## Failure Handling

If GitHub is unavailable:

- Log the failure
- Notify the administrator

If the N8N API is unavailable:

- Stop execution
- Notify the administrator

---

## Security Requirements

The workflow should:

- Use API credentials securely
- Use GitHub credentials securely
- Never expose tokens in logs

---

## Tools Required

- Schedule Trigger
- N8N API
- GitHub Node

Optional:

- Code Node
- Set Node
- Gmail Node
- Slack Node

---

# What The Learner Will Practice

By completing this project, you will learn:

### N8N API Usage

How to interact with N8N programmatically.

### Workflow Exporting

How workflow definitions are stored.

### File Handling

Creating files dynamically from workflow data.

### GitHub Integration

Uploading files and managing repositories.

### Version Control Fundamentals

Understanding commits, history, and recovery.

### Backup Automation

Protecting critical business systems.

### Production Operations

Building systems that maintain other systems.

---

# Success Criteria

The project is complete when:

- The workflow runs automatically.
- All workflows are retrieved successfully.
- JSON files are created.
- Files are committed to GitHub.
- Previous versions remain accessible.
- Administrators can restore deleted workflows from backups.

---

# Alternative Scenarios For Practice

After completing the main project, choose one of the following scenarios and build it yourself.

---

## Scenario 1 — Google Drive Backup System

A business wants important files automatically backed up from one Google Drive folder to another.

Requirements:

- Detect new files.
- Copy them to a backup location.
- Preserve folder structure.

---

## Scenario 2 — Database Backup Archiver

A company wants daily database exports stored in cloud storage.

Requirements:

- Download database dump.
- Compress the file.
- Upload to Google Drive or S3.

---

## Scenario 3 — Notion Workspace Backup

A content team wants all Notion pages exported regularly.

Requirements:

- Export page content.
- Save backups to GitHub.
- Track changes over time.

---

## Scenario 4 — Airtable Base Snapshot System

A business wants daily snapshots of Airtable records.

Requirements:

- Export all records.
- Save JSON backups.
- Keep historical versions.

---

## Scenario 5 — API Configuration Backup

An IT department wants configuration data from a third-party platform backed up daily.

Requirements:

- Call API endpoints.
- Export configuration data.
- Store in GitHub.

---

# Challenge Extensions

After completing the project, try adding one of the following:

- Create separate folders for active and inactive workflows.
- Backup workflow credentials metadata (without secrets).
- Generate a daily backup report.
- Send a Slack notification after successful backups.
- Send an email summary showing:
    - Total workflows backed up
    - New workflows detected
    - Modified workflows detected
- Automatically create GitHub releases for weekly snapshots.
- Compress workflow files before storing them.
- Store backups in both GitHub and Google Drive.
- Detect deleted workflows and alert administrators.
- Create a dashboard showing backup history.
- Track workflow size growth over time.
- Create a one-click workflow restore system.
- Store backup logs in a database.
- Generate a changelog between workflow versions using AI.
- Build a disaster recovery workflow that restores workflows automatically from GitHub.

---

# Production Insight

This project introduces one of the most important engineering principles:

**Automate the protection of your automations.**

The pattern is:

**Schedule → Export → Store → Version → Recover**

This same pattern is used for:

- Database backups
- Infrastructure backups
- Configuration backups
- Source code backups
- Document archiving
- Compliance retention systems

Many beginners focus only on creating automations.

Professional automation engineers also build systems that protect, monitor, and recover those automations when failures happen.