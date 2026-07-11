# 📩 AI Customer Support Ticket Triage — n8n Automation

![n8n](https://img.shields.io/badge/n8n-Automation-orange)
![OpenAI](https://img.shields.io/badge/AI-OpenAI-blue)
![JavaScript](https://img.shields.io/badge/Code-JavaScript-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

An AI-powered customer support automation workflow built using **n8n**, **OpenAI**, **Gmail API**, **Google Sheets**, and **Telegram Bot API**.

This system automatically monitors incoming customer emails, detects support-related requests, filters irrelevant messages, classifies tickets using artificial intelligence, assigns departments and priorities, calculates SLA response targets, stores ticket records, and sends real-time notifications to support teams.

**Stack:**  
n8n · OpenAI · Gmail API · Google Sheets · Telegram Bot · JavaScript · Google Workspace API · AI Automation


---

# 🎯 Project Overview


## Problem

Customer support teams receive a large number of emails every day, including:


- Technical issues
- Account problems
- Billing requests
- General inquiries
- Spam messages
- Marketing emails


Manually reviewing and categorizing every message creates several challenges:


- Slow response times
- Incorrect ticket prioritization
- Missed urgent customer issues
- Increased workload for support teams
- Difficult ticket tracking


Common support tasks affected:


- Email classification
- Ticket assignment
- Priority management
- SLA tracking
- Customer communication


---

## Solution

This project creates an AI-powered ticket triage system that automatically:


1. Monitors incoming Gmail messages
2. Filters irrelevant emails
3. Extracts customer request information
4. Uses OpenAI to classify support tickets
5. Assigns departments and priority levels
6. Generates SLA response targets
7. Stores ticket information in Google Sheets
8. Sends Telegram notifications to support teams


The workflow acts as an intelligent support assistant that helps teams process customer requests faster and maintain consistent service quality.


---

# ✨ Features


## Email Processing

✅ Gmail inbox monitoring  
✅ Automatic email detection  
✅ Support request identification  
✅ Email content extraction  
✅ Spam and irrelevant email filtering  


## Artificial Intelligence

✅ OpenAI-powered ticket analysis  
✅ Customer issue classification  
✅ Department assignment  
✅ Priority prediction  
✅ AI-generated summaries  
✅ SLA response recommendation  


## Ticket Management

✅ Automated ticket creation  
✅ Google Sheets ticket database  
✅ Structured ticket records  
✅ Status tracking  
✅ Support workflow automation  


## Notifications

✅ Telegram support alerts  
✅ High-priority ticket notifications  
✅ Real-time team updates  


---

# 🗺️ System Architecture


```mermaid
flowchart TD


A["📩 Customer Email"]

--> B["📧 Gmail Trigger"]


B --> C{"🚫 Email Filter"}


C -->|Spam / Newsletter| D["❌ Ignore Email"]


C -->|Support Request| E["🤖 OpenAI Analysis"]


E --> F["📝 JavaScript JSON Parser"]


F --> G["🏷️ Assign Department"]


G --> H["⚡ Priority + SLA Generator"]


H --> I["📊 Google Sheets Ticket Database"]


I --> J["📱 Telegram Notification"]

````

---

# 🏗️ Workflow Implementation

# Workflow 1: AI Support Ticket Processing Pipeline

## Node 1 — Gmail Trigger

### Purpose

Monitor incoming customer emails and start the support workflow automatically.

Configuration:

```text
Trigger:

Gmail Trigger


Event:

New Email Received
```

Captured Information:

| Field     | Description            |
| --------- | ---------------------- |
| Sender    | Customer email address |
| Subject   | Email title            |
| Body      | Customer message       |
| Labels    | Gmail metadata         |
| Timestamp | Email received time    |

Example:

```json
{
"sender":
"customer@email.com",

"subject":
"Unable to login",

"message":
"I cannot access my account."
}
```

---

# Node 2 — IF Node (Email Filtering)

### Purpose

Identify whether an email is a valid customer support request.

Filtered Messages:

* Newsletters
* Marketing emails
* Automated notifications
* Promotional messages

Logic:

```text
Incoming Email

        ↓

Support Request?

        ↓

YES → Continue Processing

NO → Ignore Email
```

---

# Node 3 — OpenAI Ticket Classification

### Purpose

Analyze customer messages and generate structured support ticket information.

AI Evaluation Criteria:

* Customer issue
* Department
* Priority
* Urgency
* Required response time
* Customer impact

Example AI Response:

```json
{
"department":
"Technical Support",

"priority":
"High",

"summary":
"Customer cannot login to account.",

"sla":
"Respond within 1 hour"
}
```

AI Output:

| Field      | Description                |
| ---------- | -------------------------- |
| Department | Assigned support team      |
| Priority   | Ticket urgency             |
| Summary    | AI-generated issue summary |
| SLA        | Response target            |

---

# Node 4 — Code Node (JSON Parser)

### Purpose

Convert AI-generated output into structured n8n workflow data.

Processing:

```text
OpenAI Response

        ↓

JavaScript JSON Parsing

        ↓

Structured Ticket Data
```

Example Output:

```json
{
"department":
"Technical Support",

"priority":
"High",

"summary":
"Login problem"
}
```

---

# Node 5 — IF Node (Ticket Validation)

### Purpose

Confirm whether the message should become an official support ticket.

## TRUE Branch

Continue processing:

* Generate ticket metadata
* Store ticket record
* Notify support team

## FALSE Branch

Ignore message.

---

# Node 6 — Set Node (Ticket Metadata)

### Purpose

Generate additional ticket information.

Generated Fields:

| Field        | Description          |
| ------------ | -------------------- |
| Priority     | Ticket urgency       |
| SLA          | Response deadline    |
| Status       | Current ticket state |
| Created Date | Ticket timestamp     |

Example:

```text
Priority:

High


SLA:

1 Hour


Status:

Open
```

---

# Node 7 — Google Sheets

### Purpose

Store customer support tickets for tracking and management.

Database Structure:

| Field      | Description          |
| ---------- | -------------------- |
| Date       | Ticket creation date |
| Sender     | Customer email       |
| Subject    | Ticket title         |
| Department | Assigned team        |
| Priority   | Urgency level        |
| Summary    | AI issue summary     |
| SLA        | Response target      |
| Status     | Ticket state         |

Example:

| Customer                                        | Department        | Priority | SLA      | Status |
| ----------------------------------------------- | ----------------- | -------- | -------- | ------ |
| [customer@email.com](mailto:customer@email.com) | Technical Support | High     | 1 Hour   | Open   |
| [client@email.com](mailto:client@email.com)     | Billing           | Medium   | 24 Hours | Open   |

---

# Node 8 — Telegram Notification

### Purpose

Send instant alerts to support teams when new tickets are created.

Example:

```text
🚨 New Support Ticket


🏷️ Department:

Technical Support


⚡ Priority:

High


📝 Summary:

Customer cannot login to account.


⏱️ SLA:

Respond within 1 hour


📌 Status:

Open
```

---

# 📊 Ticket Management Database

Google Sheets stores:

| Field          | Description         |
| -------------- | ------------------- |
| Ticket Date    | Creation timestamp  |
| Customer Email | User contact        |
| Issue Category | Support type        |
| Department     | Assigned team       |
| Priority       | Urgency level       |
| SLA            | Response deadline   |
| Status         | Ticket progress     |
| Summary        | AI-generated report |

---

# 🔐 Credentials Required

| Service          | Purpose                  |
| ---------------- | ------------------------ |
| Gmail OAuth2     | Email monitoring         |
| OpenAI API       | AI ticket classification |
| Google OAuth2    | Google Sheets storage    |
| Telegram Bot API | Team notifications       |
| n8n Instance     | Workflow execution       |

---

# ⚙️ Setup Guide

## 1. Configure Gmail

Connect Gmail OAuth credentials inside n8n.

Required permission:

```text
Read Emails
```

Test incoming email detection.

---

## 2. Configure OpenAI

Add OpenAI API credentials:

```text
OPENAI_API_KEY
```

Test ticket classification response.

---

## 3. Create Google Sheets Database

Create spreadsheet:

```text
Customer Support Tickets
```

Required columns:

```text
Date

Sender

Subject

Department

Priority

Summary

SLA

Status
```

---

## 4. Configure Telegram Bot

Steps:

1. Open Telegram
2. Create bot using BotFather
3. Copy bot token
4. Add Telegram credentials in n8n
5. Configure notification channel

---

## 5. Import Workflow

Import:

```text
workflow.json
```

Configure:

* Gmail credential
* OpenAI credential
* Google Sheets credential
* Telegram credential

Activate workflow.

---

# 🧪 Testing Checklist

| Test Case              | Expected Result         |
| ---------------------- | ----------------------- |
| Receive support email  | Workflow starts         |
| Receive newsletter     | Email filtered          |
| OpenAI analyzes ticket | Classification created  |
| High priority ticket   | Telegram alert sent     |
| Google Sheets updated  | Ticket stored           |
| SLA generated          | Response target created |

---

# 📁 Repository Structure

```text
AI-Customer-Support-Ticket-Triage/

│
├── README.md
│
├── workflow.json
│
├── screenshots/
│   │
│   ├── workflow.png
│   ├── gmail-trigger.png
│   ├── email-filter.png
│   ├── openai-output.png
│   ├── code-node-output.png
│   ├── if-node.png
│   ├── google-sheets-result.png
│   ├── telegram-notification.png
│   └── execution-result.png
│
└── assets/
    │
    └── sample-ticket.json
```

---

# 📸 Screenshots

Recommended screenshots:

* Complete n8n workflow
* Gmail Trigger configuration
* Email filtering logic
* OpenAI classification output
* JSON parser result
* Ticket routing logic
* Google Sheets ticket database
* Telegram notification
* Workflow execution result

---

# 🚀 Future Improvements

| Feature                   | Implementation                 |
| ------------------------- | ------------------------------ |
| Auto Email Reply          | Generate AI customer responses |
| Ticket ID System          | Unique ticket tracking         |
| Sentiment Analysis        | Detect customer emotions       |
| CRM Integration           | Salesforce/Zendesk connection  |
| Support Dashboard         | Analytics dashboard            |
| Knowledge Base AI         | Automated troubleshooting      |
| Multi-language Support    | Global customer service        |
| Voice Support Integration | AI call transcription          |

---

# 🎓 Skills Applied

## Automation

* n8n Workflow Automation
* Event-driven workflows
* Business process automation
* Customer support automation

## Artificial Intelligence

* OpenAI API Integration
* Prompt Engineering
* AI classification systems
* Structured AI outputs

## Programming

* JavaScript
* JSON processing
* Data transformation
* Workflow logic

## APIs

* Gmail API
* Google Sheets API
* Telegram Bot API

## Business Automation

* Ticket management systems
* SLA-based routing
* AI-assisted customer support

---

# 📚 Learning Objectives

This project demonstrates:

* Building AI-powered customer support systems
* Automating email classification workflows
* Integrating LLMs into business processes
* Creating SLA-based ticket routing
* Designing scalable n8n automation solutions

---

# 🙌 Acknowledgements

* n8n
* OpenAI
* Gmail API
* Google Sheets API
* Telegram Bot API

---

# 👨‍💻 Author

**Belio C. Sinangote**

BS Information Technology Student
Cebu Technological University (CTU)

GitHub:

[https://github.com/belioautomation](https://github.com/belioautomation)

This project is part of my **30-Day n8n Automation Portfolio**, showcasing AI-powered workflow automation using **n8n, OpenAI, APIs, JavaScript, and real-world business automation systems**.

---

# 📄 License

MIT License

```
```
