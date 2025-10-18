🚀 Lead Qualifier & AI Intent Classifier

Welcome to your Lead Qualifier party 🤖🎉! This n8n-powered workflow is here to catch incoming leads from your Gmail, analyze their buying intent with AI, and then log and alert your team accordingly. It’s like having a smart assistant sorting your leads for you while you sip your latte ☕!

🔮 Project Vibe & What It Automates

Get ready to automate the snooze-worthy task of sorting email leads. Here's the vibe:

Smart Filtering: Every new email (aka “potential lead”) triggers this flow.

AI Brainpower: OpenAI (GPT-4) reads each email and says: “High Intent? Low Intent? Why so?”.

Two Flows:

If High Intent, we ping it to a High Priority sheet and notify your team in Slack 🚨.

Otherwise, we schedule a demo email and still keep your CRM updated 📊.

It’s all wrapped in n8n (an open-source automation ninja), using Gmail, Google Sheets, Slack, and OpenAI. The end result? Automated lead sorting and fast follow-ups, with you as the hero who set it up. 🎯

🛠 Tools & Tech

Here’s the tech mix powering this:

n8n (workflow automation platform) 🤖

Gmail – for incoming leads and sending out demo links 📧

Google Sheets – your (cloud) CRM spreadsheet 📑

Slack – team notifications in a #new-lead channel 📣

OpenAI (GPT-4) – brain of the operation classifying intent 🤓🤖

n8n Workflows 🖇️ – We use two flows: the main Lead Qualification flow and a Lead Intent Classification subflow.

Make sure you have accounts or API creds ready for each. (We’ll remind you to swap out any demo IDs or dummy creds below! 😉)

⚙️ Setup Steps (Get This Rolling)

Import the Workflows: In your n8n editor, go to Workflow → Import from file and add both workflow JSONs (Lead Qualification and Lead Intent Classification).

Add Credentials:

Gmail: Connect your Gmail to n8n (OAuth). This handles email triggers and sending.

Google Sheets: Add your Google account to n8n. You’ll need to paste your own spreadsheet ID into the workflow.

Slack: Connect your Slack workspace in n8n. Create a channel (e.g. #new-lead) and grab its Channel ID to use in the Slack node.

OpenAI: Link your OpenAI API key as a credential (we’re using GPT-4.1-mini).

Configure Google Sheets:

Create a new Google Sheet (your CRM). Make two tabs: High Intent and All Leads.

In both sheets, add columns: Timestamp, Name, Email, Company, Message, Intent, Confidence.

Copy the spreadsheet ID from the URL (the long string in docs.google.com/spreadsheets/d/...) and paste it into both Google Sheets nodes.

For the High Intent node, set Sheet Name to your High Intent tab. For All Leads, set it to the All Leads tab (or use the gid).

Replace Demo Values 🤓:

Swap out any example IDs (like the demo spreadsheet ID or Slack channel ID) with yours.

Make sure the Gmail trigger is monitoring the right inbox or label for leads.

Turn Them On! 🟢

Save and activate both workflows in n8n.

Send a test email to your Gmail and watch the magic happen.

🛑 Heads Up: Double-check all credentials and IDs. If something’s off (e.g. wrong sheet ID), the flow might break. 🔍

📊 How It Works (Step by Step)

1️⃣ New Lead Arrives (Gmail Trigger): When a new email lands, n8n grabs it. The workflow extracts key info: sender name, email, company, and the message content.

2️⃣ AI-Powered Intent Check: That message text is sent to our Lead Intent Classification sub-workflow (AI). GPT-4 reads the email and spits back JSON like {intent: High/Medium/Low, confidence: ##%, reason: "..."}.

3️⃣ Branching Logic: The main workflow looks at the AI’s intent result.

If High Intent: We append the lead (timestamp, name, email, etc.) to the High Intent sheet in Google Sheets. Then a formatted Slack alert fires off (team, look alive! 🚨).

If not high: We don’t put it in High Intent for now; instead we’ll trigger the demo-scheduling email.

4️⃣ Follow-Up Email & Logging:

For any lead (high or not), we append it to the "All Leads" sheet with all details.

If it was not High Intent, we also send out a friendly Gmail inviting them to book a demo.

🎨 Workflow Diagrams (Placeholders)

(Imagine nifty flowcharts here showing the steps!)

Lead Qualification Flow:

A new email triggers the workflow; key info (name, email, company, message) is extracted.

The email text is sent to the Lead Intent Classification sub-workflow (AI).

If High Intent: add the lead to the High Intent sheet 📑 and send a Slack alert 🚨.

If not high: skip the sheet (for now) and send the demo email instead.

In all cases: append the lead to the All Leads sheet (timestamped).

Intent Classification Sub-Flow:

Takes the email text and runs GPT-4 on it.

Outputs a JSON with intent (High/Medium/Low), confidence %, and a brief reason.

📝 Final Checklist

✅ Imported workflows into n8n.

✅ Set up all credentials (Gmail, Slack, Google, OpenAI).

✅ Configured Google Sheets with your own ID and sheet names.

✅ Updated placeholder IDs (Slack channel, sheet ID, etc.).

✅ Activated both workflows.

Once all the ✅s are ticked, send a test email and see it in action! 🎉 🚀 Happy automating!
