# 🧾 Lead Qualification Automation with n8n

## 📘 Overview
This workflow automates the **lead qualification process** from incoming emails.  
It connects **Gmail**, **OpenAI**, **Google Sheets**, **Slack**, and **Google Calendar** to handle leads end-to-end — from extraction to categorization, response, and team notifications.

---

## ⚙️ Workflow Summary

| Step | Description |
|------|--------------|
| **1. Gmail Trigger** | Starts the workflow when a new email (lead inquiry) arrives in Gmail. |
| **2. Information Extractor (AI)** | Extracts name, email, company, and message content using OpenAI or a Function node. |
| **3. Intent Classifier (AI)** | Uses OpenAI to analyze the lead’s message and classify it as **High Intent**, **Medium Intent**, or **Low Intent**. |
| **4. Branching Logic** | Routes leads based on the classification result. |
| **5. High Intent Branch** | Adds the lead details to a Google Sheet CRM for the sales team to follow up. |
| **6. Medium/Low Intent Branch** | Sends an automated Gmail response inviting the lead to schedule a demo via a Google Calendar link. |
| **7. Slack Notification** | Sends a real-time Slack alert to the sales team with lead details and intent classification. |
| **8. Google Sheets Logging** | Logs all leads (including confidence score and reasoning) for analytics and tracking. |

---

## 🧠 Intent Classification Prompt

Below is the system message used in the OpenAI node to categorize lead intent:

```text
You are an expert lead qualification assistant.
You analyze email messages and classify their buying intent.

Classify each message strictly as:
- High Intent → wants to purchase, schedule, or discuss pricing soon.
- Medium Intent → interested but not urgent, wants more information or demo.
- Low Intent → vague inquiry, exploring, or not ready to buy.

Respond in JSON:
{
  "intent": "High Intent | Medium Intent | Low Intent",
  "confidence": 0-100,
  "reason": "Brief 1-2 sentence explanation"
}
```

---

## 📨 Automated Email Template (Medium/Low Intent)

HTML version used in Gmail node:

```html
Hi {{ $('Information Extractor').item.json.output.Name }},  
Thanks for reaching out! We'd love to show you how we can help.  
You can schedule a quick demo here:  
<a href="https://calendar.google.com/calendar/u/1/r" target="_blank">Schedule a quick demo</a>  
<br><br>  
Best,<br>Sales Team
```

---

## 📊 Google Sheets Setup

- **Sheet 1 (CRM):** For High Intent leads  
  Columns: `Timestamp | Name | Email | Company | Message | Intent | Confidence`

- **Sheet 2 (All Leads):** For tracking all intents

Make sure to connect your Google Sheets node and select the right Sheet IDs.

---

## 💬 Slack Integration

**Common Error Fix:**  
If you get `Slack error response: "not_in_channel"`, invite your bot to the target channel:
```
/invite @your-bot-name
```

**Slack message example:**
```
🚨 New Lead Received!
Name: {{ $json["name"] }}
Email: {{ $json["email"] }}
Company: {{ $json["company"] }}
Intent: {{ $json["intent"] }} (Confidence: {{ $json["confidence"] }}%)
Summary: {{ $json["reason"] }}
```

---

## 🗓️ Google Calendar Integration

You can optionally create an event automatically for Medium/Low Intent leads:
- Use the **Google Calendar → Create Event** node
- Add attendee: `{{$json["email"]}}`
- Use your booking link in the response email

---

## 🧩 Nodes Used

- **Gmail (Trigger + Send Email)**  
- **OpenAI (Chat / Text Generation)**  
- **Google Sheets (Append Row)**  
- **Slack (Send Message)**  
- **Google Calendar (Optional: Create Event)**  
- **IF Node / Switch Node** for branching by intent

---

## 🧰 Setup Instructions

1. Connect integrations:
   - Gmail  
   - Google Sheets  
   - Slack (with `chat:write` permission)  
   - OpenAI (with valid API key)
2. Copy the provided workflow to n8n.
3. Paste the intent classification prompt in your OpenAI node.
4. Update Google Sheet and Slack channel references.
5. Execute once manually → then activate the workflow.

---

## 🚀 Result

With this automation:
- Every new lead email is instantly analyzed and categorized.
- High Intent leads go straight into CRM.
- Medium/Low Intent leads get automated follow-ups.
- Sales team gets notified in Slack with all lead info.
- Full tracking happens in Google Sheets.

---

👨‍💻 **Author:** Pratyush Kumar Jha  
**Tools Used:** n8n, OpenAI, Google Workspace, Slack API  
**License:** MIT
