---

# 📩 AI Customer Support Ticket Triage (n8n Automation)

An intelligent automation system built using **n8n + OpenAI + Gmail + Google Sheets + Telegram** that automatically detects, classifies, and routes customer support emails.

---

## 🚀 Overview

This workflow automatically:

* Monitors incoming Gmail messages
* Filters out non-support emails (LinkedIn, newsletters, etc.)
* Uses AI (OpenAI) to classify support tickets
* Assigns department + priority + summary
* Generates SLA response time
* Stores tickets in Google Sheets
* Sends real-time alerts via Telegram

---

## ⚙️ Workflow Architecture

```text
Gmail Trigger
      ↓
IF (Not LinkedIn / Not Spam)
      ↓
OpenAI (Ticket Classification)
      ↓
Classify Ticket (Parse JSON)
      ↓
IF (department != Ignore)
      ↓
Set Priority + SLA
      ↓
Google Sheets (Log Ticket)
      ↓
Telegram Alert (Notify Team)
```

---

## 🧠 Features

* 🤖 AI-powered email classification (OpenAI)
* 📊 Automated ticket logging (Google Sheets)
* ⏱️ SLA-based priority system
* 🚫 Smart filtering (LinkedIn, newsletters, promotions)
* 📢 Real-time alerts via Telegram
* 🔁 Fully automated workflow (no manual handling)

---

## 📦 Tech Stack

* [n8n](https://n8n.io/)
* Gmail API
* OpenAI API (GPT-4 / GPT-4o-mini)
* Google Sheets API
* Telegram Bot API

---

## 🧩 Workflow Nodes

### 1. Gmail Trigger

Listens for new incoming emails in the inbox.

**Key fields used:**

* From
* Subject
* Snippet
* Labels

---

### 2. IF Node (Filter Emails)

Filters out non-support emails.

### Condition:

```javascript
{{ $json.From }}
```

**Rule:**

* Does NOT contain `linkedin.com`

---

### 3. OpenAI Node (Classifier)

Sends email content to AI for classification.

### Prompt:

```text
Analyze this email and classify it.

Return JSON only:
{
  "department": "",
  "priority": "",
  "summary": ""
}
```

---

### 4. Classify Ticket (Code Node)

Parses OpenAI response into structured data.

````javascript
const aiResponse = $json.text;

const clean = aiResponse
  .replace(/```json/g, '')
  .replace(/```/g, '')
  .trim();

const result = JSON.parse(clean);

return [{
  json: result
}];
````

---

### 5. IF Node (Ignore Filter)

Stops non-support emails.

**Condition:**

```javascript
{{ $json.department !== "Ignore" }}
```

---

### 6. Set Priority Node

Assigns SLA and ticket status.

```javascript
SLA:
{{ 
$json.priority === "High"
? "Respond within 1 hour"
: $json.priority === "Medium"
? "Respond within 4 hours"
: "Respond within 24 hours"
}}

Status: Open
CreatedDate: {{$now}}
```

---

### 7. Google Sheets Node

Stores ticket data.

| Column     | Value                                        |
| ---------- | -------------------------------------------- |
| Date       | `{{ $json.createdDate }}`                    |
| Sender     | `{{ $('Gmail Trigger').item.json.From }}`    |
| Subject    | `{{ $('Gmail Trigger').item.json.Subject }}` |
| Department | `{{ $json.department }}`                     |
| Priority   | `{{ $json.priority }}`                       |
| Summary    | `{{ $json.summary }}`                        |
| SLA        | `{{ $json.sla }}`                            |
| Status     | `{{ $json.status }}`                         |

---

### 8. Telegram Node

Sends real-time alerts.

```text
🚨 New Support Ticket

From: {{ $('Gmail Trigger').item.json.From }}
Subject: {{ $('Gmail Trigger').item.json.Subject }}

Department: {{ $json.department }}
Priority: {{ $json.priority }}

Summary: {{ $json.summary }}
SLA: {{ $json.sla }}
```

---

## 🔀 Branch Logic

### TRUE Branch

✔ Real support tickets
✔ Sent to OpenAI and processed

### FALSE Branch

❌ LinkedIn emails
❌ Newsletters
❌ Promotions
→ Ignored or optionally logged

---

## 🛠️ Setup Instructions

### 1. Clone / Import Workflow

Import your n8n workflow JSON file.

---

### 2. Setup Credentials

* Gmail OAuth
* OpenAI API Key
* Google Sheets API
* Telegram Bot Token

---

### 3. Configure Google Sheet

Create columns:

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

### 4. Run Workflow

Activate workflow in n8n.

---

## 📊 Example Output

### Input Email:

```
Subject: Cannot login to account
Body: I am unable to access my account since yesterday.
```

### AI Output:

```json
{
  "department": "Technical Support",
  "priority": "High",
  "summary": "User cannot login"
}
```

### Google Sheet Entry:

```
High | Technical Support | User cannot login | SLA: 1 hour
```

### Telegram Alert:

```
🚨 New Support Ticket - High Priority
```

---

## 🎯 Future Improvements

* Auto-reply email system
* Ticket ID generator
* Slack integration
* AI sentiment detection
* Dashboard UI (React / Next.js)
* Multi-language support

---

## 🧑‍💻 Author

Built with ❤️ using n8n + OpenAI automation.

---
