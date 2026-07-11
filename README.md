# 📩 AI Customer Support Ticket Triage — n8n Automation

An AI-powered customer support automation workflow built using **n8n**, **OpenAI**, **Gmail**, **Google Sheets**, and **Telegram Bot API**.

This system automatically monitors incoming customer emails, filters irrelevant messages, classifies support requests using AI, assigns departments and priorities, calculates SLA response times, stores ticket records, and sends real-time notifications to support teams.

**Stack:**  
n8n · OpenAI · Gmail · Google Sheets · Telegram Bot · JavaScript · Google Workspace API


---

# 🎯 Project Overview


## Problem

Customer support teams often receive large volumes of emails containing:

- Technical issues
- Account problems
- General inquiries
- Spam messages
- Marketing emails

Manually reviewing and categorizing every message can lead to:

- Slow response times
- Incorrect ticket prioritization
- Missed urgent issues
- Increased workload


---

## Solution

This project creates an AI-powered ticket triage system that automatically:


1. Monitors incoming Gmail messages
2. Filters irrelevant emails
3. Uses AI to analyze customer requests
4. Classifies tickets by department
5. Assigns priority levels
6. Generates SLA response times
7. Stores ticket information
8. Sends instant team notifications


---

# ✨ Features


## Email Processing

✅ Gmail inbox monitoring  
✅ Automatic email filtering  
✅ Support ticket detection  
✅ Email content extraction  


## AI Ticket Classification

✅ OpenAI-powered analysis  
✅ Department assignment  
✅ Priority prediction  
✅ Ticket summarization  
✅ SLA recommendation generation  


## Automation

✅ n8n workflow automation  
✅ Google Sheets ticket database  
✅ Telegram notifications  
✅ Automated support pipeline  


---

# 🗺️ System Architecture


```mermaid
flowchart TD


A["📩 Customer Email"]

--> B["📧 Gmail Trigger"]


B --> C{"🚫 Filter Email"}


C -->|Spam / Newsletter| D["Ignore"]

C -->|Support Request| E["🤖 OpenAI Analysis"]


E --> F["📝 Parse JSON Output"]


F --> G["🏷️ Assign Department"]

G --> H["⚡ Set Priority + SLA"]


H --> I["📊 Google Sheets"]

I --> J["📱 Telegram Notification"]

````

---

# 🏗️ Workflow Implementation

# Workflow 1: AI Support Ticket Processing

## Node 1 — Gmail Trigger

### Purpose

Monitor incoming customer support emails.

Captured Information:

| Field   | Description      |
| ------- | ---------------- |
| Sender  | Customer email   |
| Subject | Email title      |
| Body    | Customer message |
| Labels  | Gmail metadata   |

Configuration:

```
Trigger:
Gmail Trigger

Event:
New Email Received
```

---

# Node 2 — IF Node (Email Filtering)

### Purpose

Remove irrelevant messages before AI processing.

Filtered Examples:

* LinkedIn notifications
* Newsletters
* Promotional emails
* Automated messages

Logic:

```
Support Email
      |
      ↓
Continue Workflow


Non-support Email
      |
      ↓
Ignore
```

---

# Node 3 — OpenAI Ticket Classification

### Purpose

Analyze customer messages and classify support requests.

AI Evaluation Criteria:

* Customer issue
* Department
* Priority
* Urgency
* Required response time

Example AI Output:

```json
{
"department":
"Technical Support",

"priority":
"High",

"summary":
"User cannot log in to account.",

"sla":
"Respond within 1 hour"
}
```

---

# Node 4 — Code Node

### Purpose

Convert AI-generated JSON output into structured n8n data.

Processing:

```
OpenAI Response

        ↓

JSON Parser

        ↓

Workflow Data
```

Output:

```json
{
"department":"Technical Support",
"priority":"High",
"summary":"Login problem"
}
```

---

# Node 5 — IF Node (Ticket Validation)

### Purpose

Determine whether the email should become a support ticket.

## TRUE

Continue processing:

* Assign SLA
* Save ticket
* Notify support team

## FALSE

Ignore message.

---

# Node 6 — Set Node

### Purpose

Generate ticket metadata.

Generated Fields:

| Field        | Description       |
| ------------ | ----------------- |
| Priority     | Ticket urgency    |
| SLA          | Response deadline |
| Status       | Ticket state      |
| Created Date | Timestamp         |

Example:

```
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

Store support tickets for tracking.

Database Structure:

| Field      | Description          |
| ---------- | -------------------- |
| Date       | Ticket creation date |
| Sender     | Customer email       |
| Subject    | Ticket title         |
| Department | Assigned team        |
| Priority   | Urgency level        |
| Summary    | AI summary           |
| SLA        | Response target      |
| Status     | Ticket status        |

---

# Node 8 — Telegram Notification

### Purpose

Notify support teams instantly.

Example:

```
🚨 New Support Ticket


Department:
Technical Support


Priority:
High


Summary:
User cannot log in to account.


SLA:
Respond within 1 hour
```

---

# 📊 Ticket Management Sheet

Example:

| Customer                                    | Department        | Priority | SLA      | Status |
| ------------------------------------------- | ----------------- | -------- | -------- | ------ |
| [user@email.com](mailto:user@email.com)     | Technical Support | High     | 1 Hour   | Open   |
| [client@email.com](mailto:client@email.com) | Billing           | Medium   | 24 Hours | Open   |

---

# 🔐 Credentials Required

| Service       | Purpose            |
| ------------- | ------------------ |
| Gmail OAuth2  | Email monitoring   |
| OpenAI API    | AI classification  |
| Google OAuth2 | Sheets storage     |
| Telegram API  | Notifications      |
| n8n Instance  | Workflow execution |

---

# ⚙️ Setup Guide

## 1. Configure Gmail

Connect Gmail OAuth credentials in n8n.

Required permission:

```
Read Emails
```

---

## 2. Setup OpenAI

Add OpenAI API credentials:

```
OPENAI_API_KEY
```

Test AI response generation.

---

## 3. Create Google Sheets Database

Create spreadsheet:

```
Customer Support Tickets
```

Add columns:

```
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

## 4. Setup Telegram Bot

Steps:

1. Open Telegram
2. Create bot using BotFather
3. Copy API token
4. Add credentials in n8n
5. Configure notification channel

---

## 5. Import Workflow

Import:

```
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

| Test Case             | Expected Result          |
| --------------------- | ------------------------ |
| Receive support email | Workflow triggers        |
| Receive newsletter    | Email ignored            |
| AI analyzes ticket    | Classification generated |
| High priority ticket  | Telegram alert sent      |
| Google Sheets updated | Ticket stored            |
| SLA generated         | Response target created  |

---

# 📁 Repository Structure

```
AI-Customer-Support-Ticket-Triage/

│
├── README.md
│
├── workflow.json
│
└── screenshots/
    │
    ├── workflow.png
    ├── gmail-trigger.png
    ├── openai-output.png
    ├── code-node.png
    ├── if-node.png
    ├── google-sheets-result.png
    ├── telegram-notification.png
    └── execution-result.png
```

---

# 📸 Screenshots

Recommended screenshots:

* Complete n8n workflow
* Gmail Trigger
* Email filtering logic
* OpenAI classification output
* JSON parsing
* IF node routing
* Google Sheets ticket log
* Telegram notification
* Workflow execution

---

# 🚀 Future Improvements

| Feature                | Implementation                |
| ---------------------- | ----------------------------- |
| Auto Email Reply       | Generate AI responses         |
| Ticket ID System       | Unique ticket tracking        |
| Sentiment Analysis     | Detect customer emotions      |
| CRM Integration        | Salesforce/Zendesk connection |
| Support Dashboard      | Analytics dashboard           |
| Knowledge Base AI      | Automated troubleshooting     |
| Multi-language Support | Global customer support       |

---

# 🎓 Skills Applied

## Automation

* n8n Workflow Automation
* Event-driven systems
* Business process automation

## Artificial Intelligence

* OpenAI API Integration
* Prompt Engineering
* AI Classification

## Programming

* JavaScript
* JSON Processing
* Data Transformation

## APIs

* Gmail API
* Google Sheets API
* Telegram Bot API

---

# 📚 Learning Objectives

This project demonstrates:

* Building AI-powered customer support systems
* Automating email classification
* Integrating LLMs into workflows
* Creating SLA-based routing systems
* Designing scalable business automation

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

This project is part of my **30-Day n8n Automation Portfolio**, showcasing AI-powered workflow automation using n8n, OpenAI, APIs, and real-world business automation.

---

# 📄 License

MIT License

```

This README is now consistent with your previous automation projects and presents the workflow more like a **real AI automation engineer portfolio project** rather than only a workflow description.
```
