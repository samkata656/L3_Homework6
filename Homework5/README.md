# L3 Homework 5: Support Ticket Router with Human Support

An n8n workflow that receives support tickets through a form, rates their urgency, routes them to a department, asks a person to confirm the urgency in Telegram, then has an AI Agent write a reply, log the ticket in Google Sheets and create a Google Task.

## Files

- [`workflows/support-ticket-router.json`](workflows/support-ticket-router.json) is the workflow.
- [`data/tickets.csv`](data/tickets.csv) contains the Google Sheet column headers.

## Flow

Form → Sentiment Analysis (Critical / Negative / Neutral / Positive) → Text Classifier (Sales / Technical / Billing / General) → Telegram: confirm the sentiment or choose a new one → AI Agent with two tools: **Save to Google Sheet** and **Create Google Task**

## Setup

1. Import `tickets.csv` into a new Google Sheet: **File → Import → Upload**.
2. Import the workflow and select your Anthropic, Telegram, Google Sheets and Google Tasks credentials.
3. In both Telegram nodes, replace the **Chat ID** with your own.
4. In **Save to Google Sheet**, select your sheet. In **Create Google Task**, select your task list.
5. Open the form and submit a ticket. The sticky note includes 10 test tickets.
