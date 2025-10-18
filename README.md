# 🚀 Lead Qualifier & AI Intent Classifier

Welcome to your **Lead Qualifier** party 🤖🎉!  
This n8n-powered workflow is here to **catch incoming leads from your Gmail**, **analyze their buying intent with AI**, and then **log and alert your team** accordingly.  

It’s like having a smart assistant sorting your leads for you while you sip your latte ☕!

---

## 🔮 Project Vibe & What It Automates

Get ready to automate the snooze-worthy task of sorting email leads. Here's the vibe:

- **Smart Filtering**: Every new email (aka “potential lead”) triggers this flow.  
- **AI Brainpower**: OpenAI (GPT-4) reads each email and says: “High Intent? Low Intent? Why so?”.  
- **Two Flows**:  
  - If *High Intent*, we ping it to a **High Priority** sheet and notify your team in Slack 🚨.  
  - Otherwise, we schedule a demo email and still keep your CRM updated 📊.  

It’s all wrapped in **n8n** (an open-source automation ninja), using **Gmail**, **Google Sheets**, **Slack**, and **OpenAI**.  
The end result? Automated lead sorting and fast follow-ups, with you as the hero who set it up. 🎯

---

## 🛠 Tools & Tech

Here’s the tech mix powering this:

- **n8n** (workflow automation platform) 🤖  
- **Gmail** – for incoming leads and sending out demo links 📧  
- **Google Sheets** – your (cloud) CRM spreadsheet 📑  
- **Slack** – team notifications in a `#new-lead` channel 📣  
- **OpenAI (GPT-4)** – brain of the operation classifying intent 🤓🤖  
- **n8n Workflows** 🖇️ – We use two flows: the main **Lead Qualification** flow and a **Lead Intent Classification** subflow.

> Make sure you have accounts or API creds ready for each.  
> _(We’ll remind you to swap out any demo IDs or dummy creds below! 😉)_

---

## ⚙️ Setup Steps (Get This Rolling)

1. **Import the Workflows**  
   In your n8n editor, go to **Workflow → Import from file** and add both workflow JSONs:  
   - `Lead Qualification`  
   - `Lead Intent Classification`  

2. **Add Credentials**  
   - **Gmail**: Connect your Gmail to n8n (OAuth).  
   - **Google Sheets**: Add your Google account to n8n and use your spreadsheet ID.  
   - **Slack**: Connect your Slack workspace. Get the Channel ID for `#new-lead`.  
   - **OpenAI**: Use your API key for GPT-4.1-mini.  

3. **Configure Google Sheets**  
   - Create a new Google Sheet with two tabs: `High Intent` and `All Leads`.  
   - Add columns: `Timestamp`, `Name`, `Email`, `Company`, `Message`, `Intent`, `Confidence`.  
   - Grab the spreadsheet ID from the URL (`docs.google.com/spreadsheets/d/...`)  
   - Paste the ID into both Google Sheets nodes in n8n.  
   - Set correct sheet names or `gid` values in each node.  

4. **Replace Demo Values 🤓**  
   - Update all demo spreadsheet IDs, Slack channel IDs, etc.  
   - Make sure the Gmail trigger watches the right inbox or label.  

5. **Turn Them On! 🟢**  
   - Save and activate both workflows.  
   - Send a test email to see the automation in action.  

> 🛑 **Heads Up**: Double-check all credentials and IDs. If something’s off (like a wrong sheet ID), things might break. 🔍

---

## 📊 How It Works (Step by Step)

1️⃣ **New Lead Arrives (Gmail Trigger)**  
→ A new email lands in Gmail → n8n grabs it.  
→ Extracts: Name, Email, Company, Message.  

2️⃣ **AI-Powered Intent Check**  
→ Message text goes to the **Lead Intent Classification** sub-workflow.  
→ GPT-4 responds with:
```json
{ 
  "intent": "High/Medium/Low", 
  "confidence": 87, 
  "reason": "They asked to book a demo this week." 
}'''

### 3️⃣ Branching Logic

- **If High Intent:**
  - Log in **High Intent** sheet.  
  - Notify in **Slack** (`#new-lead`).  

- **If not High:**
  - Skip that sheet.  

---

### 4️⃣ Follow-Up Email & Logging

- **All leads** go into the **All Leads** sheet.  
- **Non-high leads** also get a friendly demo-scheduling Gmail ✉️.  

---

### 📝 Final Checklist

✅ Imported workflows into **n8n**  
✅ Set up credentials (**Gmail**, **Slack**, **Google Sheets**, **OpenAI**)  
✅ Configured Sheets with your own IDs and sheet names  
✅ Replaced all placeholder IDs  
✅ Activated the workflows  

---

Once all that’s ✅ — go send yourself a test lead and watch the automation come to life!  
🎉🚀 **Happy automating!**
