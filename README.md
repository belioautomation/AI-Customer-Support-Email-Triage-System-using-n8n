# 📄 AI Customer Support Email Triage System using n8n

![n8n](https://img.shields.io/badge/n8n-Automation-orange)
![OpenRouter](https://img.shields.io/badge/AI-OpenRouter-blue)
![JavaScript](https://img.shields.io/badge/Code-JavaScript-yellow)
![Gmail](https://img.shields.io/badge/Google-Gmail-red)
![Google%20Sheets](https://img.shields.io/badge/Google-Sheets-green)
![MIT](https://img.shields.io/badge/License-MIT-brightgreen)

An AI-powered customer support automation workflow built using **n8n**, **OpenRouter AI**, **JavaScript**, **Gmail API**, and **Google Sheets**.

The workflow automatically monitors incoming customer emails, extracts important information, generates unique support ticket IDs, classifies each email using Artificial Intelligence, stores tickets inside Google Sheets, and automatically routes notifications to the appropriate department including **Billing**, **Technical**, **Sales**, and **General Support**.

---

# 🎯 Project Overview

## Problem

Customer support teams receive numerous emails every day from customers requesting assistance with technical issues, billing concerns, product inquiries, account management, refunds, and general questions.

Manually reviewing every email creates several challenges:

- Reading every email individually
- Determining the correct department
- Prioritizing urgent requests
- Creating support tickets manually
- Updating ticket databases
- Routing emails to the correct team
- Maintaining consistent classifications
- Delayed response times

As the number of incoming emails grows, customer support becomes increasingly difficult to manage efficiently.

---

# 💡 Solution

This project automates the customer support triage process using Artificial Intelligence.

Instead of manually reviewing every email, the workflow automatically:

1. Monitors incoming Gmail messages.
2. Extracts customer information.
3. Generates a unique support ticket.
4. Uses AI to classify the email.
5. Determines the ticket category.
6. Assigns a priority level.
7. Detects customer sentiment.
8. Identifies customer intent.
9. Determines the responsible department.
10. Stores the ticket inside Google Sheets.
11. Sends an email notification to the correct support team.

The result is a fully automated AI-powered customer support assistant capable of reducing repetitive manual work while improving response speed and ticket organization.

---

# ✨ Features

## Email Automation

- ✅ Gmail Trigger Integration
- ✅ Automatic Email Monitoring
- ✅ Email Metadata Extraction
- ✅ Customer Information Extraction
- ✅ Automatic Ticket Generation
- ✅ Unique Ticket ID Creation

---

## Artificial Intelligence

- ✅ AI Email Classification
- ✅ Ticket Categorization
- ✅ Priority Detection
- ✅ Customer Sentiment Analysis
- ✅ Customer Intent Recognition
- ✅ Team Assignment
- ✅ AI Ticket Summary
- ✅ Human Review Detection
- ✅ Confidence Score Prediction

---

## Ticket Management

- ✅ Automatic Ticket Creation
- ✅ Ticket Status Tracking
- ✅ Google Sheets Database
- ✅ Organized Ticket Records
- ✅ AI Classification Results
- ✅ Customer History Storage

---

## Workflow Automation

- ✅ Gmail Trigger Automation
- ✅ Automatic Ticket ID Generation
- ✅ Structured Output Parser
- ✅ Merge Node
- ✅ Google Sheets Ticket Database
- ✅ Switch-based Department Routing
- ✅ Billing Team Notification
- ✅ Technical Team Notification
- ✅ Sales Team Notification
- ✅ General Support Notification
- ✅ Human Review Detection
- ✅ Telegram Escalation
- ✅ Customer Auto Reply
---

# 🗺️ System Architecture

```mermaid
flowchart TD

A[Customer Sends Email]

--> B[Gmail(Customer)]

B --> C[Extract Email Details]

C --> D[Generate Ticket ID]

D --> E[AI Agent]

E --> F[Structured Output Parser]

F --> G[Merge Ticket Data]

G --> H[Create Ticket Database]

H --> I{Switch: Category}

I -->|Billing| J[Gmail Notify (Billing)]

I -->|Technical| K[Gmail Notify (Technical)]

I -->|Sales| L[Gmail Notify (Sales)]

I -->|General| M[Gmail Notify (General)]

J --> N{Requires Human?}

N -->|Yes| O[Telegram Notification]

O --> P[Customer Auto Reply]
```

---

# 🏗 Workflow Implementation

This workflow is composed of multiple automation nodes that work together to process every incoming customer email from start to finish.

Each node has a specific responsibility, beginning with email collection and ending with automated department notification and ticket storage.

The following sections explain each node in detail.

---
# 🏗 Workflow Implementation

## Node 1 — Gmail(Customer)

### Purpose

The Gmail Trigger continuously monitors the inbox for newly received customer emails. Whenever a new email arrives, the workflow is automatically executed without any manual intervention.

This serves as the starting point of the automation.

Captured Information

- Message ID
- Thread ID
- Sender Name
- Sender Email
- Recipient
- Subject
- Email Body
- Received Timestamp
- Gmail Labels

Output Example

```text
From:
john.doe@email.com

Subject:
Unable to access my account

Message:
I cannot log in after resetting my password.
```

---

## Node 2 — Extract Email Details

### Purpose

The incoming Gmail payload contains a large amount of metadata that is unnecessary for customer support processing.

This node extracts only the important customer information required by the AI and the ticketing system.

Extracted Fields

- Customer Name
- Customer Email
- Subject
- Message
- Received Timestamp
- Message ID

Example Output

```json
{
  "customer_name": "John Doe",
  "customer_email": "john@email.com",
  "subject": "Unable to access my account",
  "message": "I cannot log in after resetting my password.",
  "received_at": "1784089319000",
  "message_id": "19f617cfeaaae9f8"
}
```

---

## Node 3 — Generate Ticket ID (Code)

### Purpose

Each incoming email receives a unique ticket number.

The generated ticket allows every customer request to be tracked independently throughout its lifecycle.

Example Ticket IDs

```text
TKT-20260715-1967

TKT-20260715-2043

TKT-20260715-2188
```

Additional Fields Created

- Ticket ID
- Status

Default Status

```text
Open
```

Example Output

```json
{
  "ticket_id": "TKT-20260715-1967",
  "status": "Open"
}
```

---

## Node 4 — AI Agent

### Purpose

The AI Agent is responsible for analyzing the customer's email and automatically classifying the support request.

Using OpenRouter AI, the model determines the appropriate category, urgency, customer sentiment, intended department, and summarizes the request.

The AI evaluates

- Ticket Category
- Priority
- Sentiment
- Assigned Team
- Summary
- Customer Intent
- Human Review Requirement
- Confidence Score

Allowed Categories

- Billing
- Technical
- Sales
- Refund
- Feature Request
- Bug Report
- Account
- General

Priority Levels

- Low
- Medium
- High
- Critical

Example AI Output

```json
{
  "category": "Technical",
  "priority": "High",
  "sentiment": "Frustrated",
  "assigned_team": "Engineering Team",
  "summary": "Customer cannot log into the application after resetting the password.",
  "customer_intent": "Restore account access.",
  "requires_human": true,
  "confidence": 0.96
}
```

---

## Node 5 — Merge

### Purpose

The Merge node combines the original ticket information with the AI-generated analysis.

This creates a single data object that contains all information required for storage and notification.

Merged Information

Customer Information

- Ticket ID
- Customer Name
- Customer Email
- Subject
- Message
- Status

AI Analysis

- Category
- Priority
- Sentiment
- Assigned Team
- Summary
- Customer Intent
- Requires Human
- Confidence

---

## Node 6 — Create Ticket Database

### Purpose

This node stores every processed ticket inside Google Sheets.

The spreadsheet becomes a centralized ticket database that can be searched, filtered, and reported on by the support team.

Stored Columns

- Ticket ID
- Customer Name
- Customer Email
- Subject
- Message
- Received At
- Status
- Category
- Priority
- Sentiment
- Assigned Team
- Summary
- Customer Intent
- Requires Human
- Confidence

Benefits

- Permanent ticket records
- Searchable history
- Customer tracking
- Performance reporting
- Team workload monitoring

---

## Node 7 — Switch

### Purpose

The Switch node automatically routes tickets to the appropriate department based on the AI classification.

Routing Rules

| Category | Department |
|----------|------------|
| Billing | Billing Team |
| Technical | Technical Team |
| Sales | Sales Team |
| General | General Support |

Each ticket follows only one route, ensuring that the correct department receives the notification immediately.
## Node 8 — Gmail Notify (Billing)

### Purpose

If the AI classifies the ticket as **Billing**, the workflow sends a detailed notification email to the Billing Team.

The notification contains:

- Ticket ID
- Customer Information
- Subject
- Customer Message
- AI Summary
- Customer Intent
- Priority
- Sentiment
- Confidence Score
- Human Review Status

The Billing Team can immediately review the customer's billing request.

---

## Node 9 — IF

### Purpose

After sending the billing notification, the workflow checks whether the ticket requires manual intervention.

Condition

```
requires_human == true
```

If TRUE

- Send Telegram Notification
- Send Customer Auto Reply

If FALSE

- End Workflow
---

## Node 10 — Telegram Notification

### Purpose

For billing tickets that require human review, a Telegram alert is sent to notify the support team immediately.

The notification includes:

- Ticket ID
- Customer Name
- Priority
- Summary
- Assigned Team

This allows urgent billing issues to be escalated instantly.

---

## Node 11 — Customer Auto Reply

### Purpose

After the support team has been notified, the workflow automatically sends an acknowledgment email to the customer.

The email confirms that:

- The request has been received.
- A support ticket has been created.
- The Billing Team will review the issue.
- The customer will receive a follow-up response.

This improves customer communication by providing immediate confirmation.

---
## Node 12 — Gmail Notify (Technical)

### Purpose

Technical support requests are automatically routed to the Engineering Team.

Examples include:

- Login Problems
- API Errors
- Website Issues
- Bug Reports
- System Failures
---
## Node 13 — Gmail Notify (Sales)

### Purpose

Sales-related inquiries are automatically forwarded to the Sales Team.

Examples include:

- Product Questions
- Pricing Requests
- Subscription Inquiries
- Upgrade Requests
- Partnership Opportunities

The AI-generated summary and customer intent help the Sales Team respond efficiently.
---
## Node 14 — Gmail Notify (General)

### Purpose

General customer inquiries that do not belong to Billing, Technical, or Sales are routed to the General Support Team.

Examples include:

- General Questions
- Feedback
- Information Requests
- Miscellaneous Support

This ensures every customer email reaches the appropriate department.
---

A notification email containing the ticket details and AI analysis is sent automatically.

# 📊 Ticket Database Structure

Every processed ticket is stored inside Google Sheets using the following columns.

| Column | Description |
|---------|-------------|
| Ticket ID | Unique support ticket identifier |
| Customer Name | Sender's name |
| Customer Email | Sender's email address |
| Subject | Email subject |
| Message | Customer message |
| Received At | Email timestamp |
| Status | Current ticket status |
| Category | AI classification |
| Priority | AI priority level |
| Sentiment | AI sentiment analysis |
| Assigned Team | Department responsible |
| Summary | AI-generated summary |
| Customer Intent | AI-detected customer objective |
| Requires Human | Human review indicator |
| Confidence | AI confidence score |

---

# 📧 Department Routing

| Category | Destination |
|----------|-------------|
| Billing | Billing Team Email |
| Technical | Technical Support Email |
| Sales | Sales Team Email |
| General | General Support Email |

---

# 🧠 AI Classification Fields

The AI returns structured information for every incoming email.

| Field | Description |
|---------|-------------|
| Category | Type of customer request |
| Priority | Urgency level |
| Sentiment | Customer emotion |
| Assigned Team | Responsible department |
| Summary | Brief overview of the issue |
| Customer Intent | Purpose of the email |
| Requires Human | Human review required |
| Confidence | AI confidence score |

---

# 🔄 Workflow Summary

The workflow processes every incoming customer email through the following steps:

1. Gmail(Customer) monitors the inbox for new emails.
2. Extract Email Details retrieves the required customer information.
3. Generate Ticket ID creates a unique support ticket.
4. AI Agent analyzes and classifies the email.
5. Structured Output Parser validates the AI response.
6. Merge combines the original ticket with the AI analysis.
7. Create Ticket Database stores the ticket in Google Sheets.
8. Switch routes the ticket to the correct department.
9. Billing tickets are checked for human review.
10. Billing tickets requiring manual intervention trigger a Telegram notification.
11. The customer receives an automatic acknowledgment email.
12. Technical, Sales, and General tickets are delivered directly to their respective departments.

The entire workflow is fully automated and completes within seconds, enabling consistent ticket classification, centralized tracking, and faster response times.
## Google Gmail OAuth2

Used for:

- Monitoring incoming customer emails
- Sending automated notifications to each department

Required Permissions

- Read Emails
- Send Emails

---

## Google Sheets OAuth2

Used for:

- Creating the ticket database
- Logging every processed support ticket
- Updating ticket records

Required Permissions

- Read Spreadsheet
- Write Spreadsheet

---

## OpenRouter API

The AI Agent uses OpenRouter to classify customer emails and generate structured ticket information.

Required

- OpenRouter API Key

Example Models

- GPT-4.1 Mini
- GPT-4o Mini
- Claude Sonnet
- Gemini 2.5 Flash
- DeepSeek Chat

---

## n8n

Workflow Platform

Compatible with

- n8n Cloud
- Self-hosted n8n

---

# ⚙️ Setup Guide

## Step 1 — Clone the Repository

```bash
git clone https://github.com/yourusername/AI-Customer-Support-Email-Triage-System.git
```

Open the project folder.

---

## Step 2 — Import the Workflow

Inside n8n

Import

```
workflow.json
```

The workflow will automatically create all required nodes.

---

## Step 3 — Configure Gmail

Create a Gmail OAuth2 credential.

Connect it to

- Gmail(Customer)
- Gmail (Billing)
- Gmail (Technical)
- Gmail (Sales)
- Gmail (General)

---

## Step 4 — Configure Google Sheets

Create a Google Sheets OAuth2 credential.

Connect it to

```
Create Ticket Database
```

Create a spreadsheet with the required ticket columns.

---

## Step 5 — Configure OpenRouter

Create an OpenRouter account.

Generate an API Key.

Inside the AI Agent node

Configure

- Base URL
- API Key
- Model

Example

```
Model:
GPT-4.1 Mini
```

---

## Step 6 — Configure the AI Agent

The AI Agent should receive the following customer information.

Input

- Customer Name
- Customer Email
- Subject
- Message
- Ticket ID
- Status
- Received Time

The AI returns

- Category
- Priority
- Sentiment
- Assigned Team
- Summary
- Customer Intent
- Requires Human
- Confidence

---

## Step 7 — Configure Google Sheets

Create the following columns exactly as shown.

| Column |
|---------|
| Ticket ID |
| Customer Name |
| Customer Email |
| Subject |
| Message |
| Received At |
| Status |
| Category |
| Priority |
| Sentiment |
| Assigned Team |
| Summary |
| Customer Intent |
| Requires Human |
| Confidence |

---

## Step 8 — Configure Department Emails

Update each Gmail node with the appropriate destination email.

Billing

```
billing@company.com
```

Technical

```
technical@company.com
```

Sales

```
sales@company.com
```

General Support

```
support@company.com
```

---

## Step 9 — Activate the Workflow

Once every credential has been configured,

Click

```
Activate
```

The workflow will begin monitoring incoming customer emails automatically.

---

# 🧪 Testing Checklist

| Test | Expected Result |
|------|-----------------|
| Gmail Trigger | Workflow Starts |
| Extract Email Details | Success |
| Generate Ticket ID | Ticket Created |
| AI Agent | Email Classified |
| Structured Output Parser | JSON Validated |
| Merge Node | Data Combined |
| Google Sheets | Ticket Saved |
| Switch Node | Correct Branch |
| Billing Notification | Email Sent |
| IF Node | Human Review Checked |
| Telegram Notification | Sent (Billing Only) |
| Customer Auto Reply | Sent |
| Technical Notification | Email Sent |
| Sales Notification | Email Sent |
| General Notification | Email Sent |

---

# 📂 Repository Structure

screenshots/

├── workflow.png
├── gmail-trigger.png
├── extract-email-details.png
├── generate-ticket-id.png
├── ai-agent.png
├── structured-output-parser.png
├── merge-node.png
├── create-ticket-database.png
├── switch-node.png
├── gmail-billing.png
├── if-node.png
├── telegram-notification.png
├── customer-auto-reply.png
├── gmail-technical.png
├── gmail-sales.png
├── gmail-general.png
└── successful-execution.png
---

# 📸 Recommended Screenshots

Include screenshots of the following workflow components.

- Complete Workflow
- Gmail(Customer)
- Extract Email Details
- Generate Ticket ID
- AI Agent
- Merge Node
- Google Sheets Ticket Database
- Switch Node
- Billing Email Notification
- Technical Email Notification
- Sales Email Notification
- General Support Email Notification
- Successful Workflow Execution

---

# 📈 Example Ticket Record

| Field | Example |
|---------|---------|
| Ticket ID | TKT-20260715-1967 |
| Customer Name | John Doe |
| Customer Email | john@example.com |
| Subject | Unable to login |
| Category | Technical |
| Priority | High |
| Status | Open |
| Assigned Team | Engineering Team |
| Sentiment | Frustrated |
| Confidence | 0.97 |

---

# 📊 Workflow Benefits

This automation provides several operational advantages.

- Faster customer response times
- Automatic ticket creation
- Consistent AI-based email classification
- Reduced manual workload
- Centralized ticket database
- Improved team collaboration
- Automatic department routing
- Better customer support organization
- Easily scalable workflow
- Production-ready automation
  # 🚀 Future Improvements

Although the workflow is production-ready, several enhancements can further improve its capabilities and scalability.

## Customer Support Features

- Automatic Ticket Status Updates
- Ticket Reopening Support
- Ticket Escalation Rules
- SLA Monitoring
- Auto-close Resolved Tickets
- Duplicate Ticket Detection
- Customer Satisfaction (CSAT) Surveys
- Multi-language Email Support

---

## Artificial Intelligence

- AI Suggested Replies
- Automatic Response Draft Generation
- Intent Confidence Thresholds
- AI-powered Ticket Prioritization
- Email Spam Detection
- Email Language Detection
- Sentiment Trend Analysis
- AI Knowledge Base Integration

---

## Integrations

- Slack Notifications
- Microsoft Teams Notifications
- Discord Notifications
- Microsoft Outlook Support
- PostgreSQL Ticket Database
- MySQL Support
- Airtable Integration
- Notion Ticket Dashboard

---

## Analytics Dashboard

- Daily Ticket Volume
- Weekly Ticket Reports
- Monthly Ticket Reports
- Department Performance
- Average Response Time
- Resolution Time Analytics
- Customer Satisfaction Dashboard
- AI Classification Accuracy
- Priority Distribution
- Ticket Category Distribution

---

## Local AI Support

Reduce API costs by running local Large Language Models.

Supported Platforms

- Ollama
- LM Studio
- Open WebUI
- LocalAI

Example Models

- Llama 3
- Gemma
- DeepSeek
- Qwen
- Mistral

---

## Enterprise Features

- Multi-agent Customer Support
- Role-based Access Control
- Audit Logs
- Ticket Attachments
- Knowledge Base Search
- Approval Workflows
- Human-in-the-loop Review
- Webhook Integrations
- REST API Endpoints

---

# 💼 Skills Applied

This project demonstrates practical skills across workflow automation, artificial intelligence, cloud integrations, and JavaScript development.

## Workflow Automation

- n8n Workflow Automation
- Event-driven Automation
- Conditional Routing
- Email Automation
- Process Automation
- Business Workflow Design

---

## Artificial Intelligence

- OpenRouter AI
- Prompt Engineering
- AI-powered Email Classification
- Sentiment Analysis
- Intent Recognition
- Structured JSON Output

---

## APIs

- Gmail API
- Google Sheets API
- OpenRouter API

---

## Programming

- JavaScript
- JSON Parsing
- Data Transformation
- Workflow Logic
- Error Handling

---

## Business Automation

- Customer Support Automation
- AI Ticket Classification
- Help Desk Automation
- Email Routing
- Ticket Management
- Business Process Automation

---

# 📚 Learning Objectives

This project demonstrates how to:

- Build an AI-powered customer support automation workflow
- Automatically process incoming Gmail messages
- Extract structured information from emails
- Generate unique support ticket IDs
- Design AI prompts for consistent classification
- Route emails using conditional workflow logic
- Store structured ticket records in Google Sheets
- Send automated department notifications
- Build scalable AI-powered business workflows
- Create production-ready n8n automations

---

# 🖥 Sample Workflow Output

## Example Incoming Email

```text
From:
John Doe <john@example.com>

Subject:
Unable to Login

Message:
Hello,

I recently reset my password but I'm still unable to access my account.

Please help.

Thank you.
```

---

## AI Classification Result

```json
{
  "ticket_id": "TKT-20260715-1967",
  "customer_name": "John Doe",
  "customer_email": "john@example.com",
  "subject": "Unable to Login",
  "status": "Open",
  "category": "Technical",
  "priority": "High",
  "sentiment": "Frustrated",
  "assigned_team": "Engineering Team",
  "summary": "Customer cannot access their account after resetting the password.",
  "customer_intent": "Recover account access.",
  "requires_human": true,
  "confidence": 0.97
}
```

---

## Google Sheets Record

| Ticket ID | Category | Priority | Assigned Team | Status |
|------------|----------|----------|---------------|--------|
| TKT-20260715-1967 | Technical | High | Engineering Team | Open |

---

## Technical Team Notification

```text
Subject:

[High] Technical Ticket TKT-20260715-1967

Customer:
John Doe

Issue:
Unable to Login

Summary:
Customer cannot access their account after resetting the password.

Priority:
High

Please investigate immediately.
```

---

# 🎯 Project Highlights

✔ AI-powered email classification

✔ Automatic ticket generation

✔ Intelligent department routing

✔ Google Sheets ticket database

✔ Gmail notification automation

✔ OpenRouter AI integration

✔ JavaScript data transformation

✔ Production-ready n8n workflow

✔ End-to-end customer support automation

✔ Easily customizable and scalable

---

# 🙌 Acknowledgements

Special thanks to the following technologies that made this project possible:

- n8n
- OpenRouter
- Google Gmail API
- Google Sheets API
- JavaScript
- OpenAI-compatible Language Models

---

# 👨‍💻 Author

**Belio C. Sinangote**

BS Information Technology Student

Cebu Technological University (CTU)

GitHub:

> https://github.com/belioautomation

---

This project is part of my **30-Day n8n Automation Portfolio**, showcasing practical workflow automation projects using **n8n**, **Artificial Intelligence**, **JavaScript**, and **Google Workspace APIs**.

---

# 📄 License

This project is licensed under the **MIT License**.

You are free to use, modify, and distribute this project in accordance with the terms of the MIT License.

---
