# 🚀 Lead Qualifier & AI Intent Classifier ## [Demo Link](https://drive.google.com/file/d/1YQzE-0wK7Uczb5hPoIIxj8UcliPfp9XM/view?usp=sharing)

Welcome to your **Lead Qualifier party** 🤖🎉!  
This **n8n-powered workflow** is here to catch incoming leads from your Gmail, analyze their buying intent with AI, and then log and alert your team accordingly.  

It’s like having a smart assistant sorting your leads for you while you sip your latte ☕!

---

## 🔮 Project Vibe & What It Automates

Get ready to automate the snooze-worthy task of sorting email leads. Here's the vibe:

### Smart Filtering
Every new email (aka “potential lead”) triggers this flow.

### AI Brainpower
OpenAI (GPT-4) reads each email and says:  
> “High Intent? Low Intent? Why so?”

### Two Flows:
- **If High Intent:** We ping it to a **High Priority** sheet and notify your team in **Slack** 🚨  
- **Otherwise:** We schedule a demo email and still keep your **CRM updated** 📊

It’s all wrapped in **n8n** (an open-source automation ninja), using **Gmail**, **Google Sheets**, **Slack**, and **OpenAI**.  

💡 *The end result? Automated lead sorting and fast follow-ups, with you as the hero who set it up.* 🎯

---

## 🛠 Tools & Tech

Here’s the tech mix powering this workflow:

| Tool | Purpose |
|------|----------|
| 🧩 **n8n** | Workflow automation platform |
| 📧 **Gmail** | Incoming leads + sending demo emails |
| 📑 **Google Sheets** | CRM & data logging |
| 💬 **Slack** | Team notifications |
| 🧠 **OpenAI (GPT-4)** | Classifying lead intent |
| 🔁 **n8n Subflow** | Lead Intent Classification logic |

Make sure you have accounts or API creds ready for each tool.  
*(We’ll remind you to swap out demo IDs or dummy creds below! 😉)*

---

## ⚙️ Setup Steps (Get This Rolling)

### 1. Import the Workflows
In your n8n editor:
- Go to **Workflow → Import from File**
- Add both workflow JSONs:
  - **Lead Qualification**
  - **Lead Intent Classification**

### 2. Add Credentials
- **Gmail:** Connect via OAuth for triggers and sending emails  
- **Google Sheets:** Add Google account → paste your own **Spreadsheet ID**  
- **Slack:** Connect your workspace → create channel (e.g. `#new-lead`) → get **Channel ID**  
- **OpenAI:** Link your **OpenAI API key** (we’re using `gpt-4.1-mini`)

### 3. Configure Google Sheets
Create a new Sheet (your CRM) with **two tabs**:
- `High Intent`
- `All Leads`

Add these columns in both:
```
Timestamp | Name | Email | Company | Message | Intent | Confidence
```

Then:
- Copy the **Spreadsheet ID** from the URL (`docs.google.com/spreadsheets/d/...`)
- Paste it in both Google Sheets nodes
- Set the right **Sheet Name** for each node (`High Intent` / `All Leads`)

### 4. Replace Demo Values 🤓
- Swap demo **Spreadsheet IDs** and **Slack Channel IDs** with yours  
- Ensure Gmail trigger is watching the right **inbox/label**

### 5. Turn Them On 🟢
- Save and activate both workflows in n8n  
- Send a test email to your Gmail and watch the automation magic ✨  

🛑 **Heads Up:** Double-check all credentials and IDs.  
If something’s off (like a wrong sheet ID), the flow might break. 🔍

---

## 📊 How It Works (Step-by-Step)

### 1️⃣ New Lead Arrives (Gmail Trigger)
When a new email lands, n8n grabs it.  
The workflow extracts:
- Sender name  
- Email address  
- Company  
- Message content  

---

### 2️⃣ AI-Powered Intent Check
That message text is sent to our **Lead Intent Classification sub-workflow**.  
GPT-4 reads the email and returns a JSON like:

```json
{ 
  "intent": "High/Medium/Low", 
  "confidence": 87, 
  "reason": "They asked to book a demo this week." 
}
```

---

### 3️⃣ Branching Logic
The main workflow looks at the AI’s result:

#### If **High Intent**:
- Append lead (timestamp, name, email, etc.) → **High Intent Sheet**
- Trigger **Slack alert** (team gets notified 🚨)

#### If **Not High Intent**:
- Skip the High Intent sheet  
- Send a **demo-scheduling email**

---

### 4️⃣ Follow-Up Email & Logging
- **All leads** (high or not) get logged into **All Leads sheet**  
- **Non-high leads** get a friendly follow-up email inviting them to book a demo  

---

## 📝 Final Checklist

✅ Imported both workflows into n8n  
✅ Connected all credentials (Gmail, Slack, Google, OpenAI)  
✅ Configured Google Sheets (your IDs + tab names)  
✅ Updated placeholder values (Sheet IDs, Slack IDs, etc.)  
✅ Activated both workflows  

---

Once all the ✅s are ticked, send a **test email** and watch it run in real time.  
🎉 **Happy automating, superstar!** 🚀
