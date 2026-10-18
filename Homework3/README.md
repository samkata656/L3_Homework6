# L3 Homework 3: Smart Content Categorizer

An n8n workflow that receives a batch of articles through a webhook, sorts each one into a category with AI, and builds a count per category. Spam is stopped with an error and reported by email.

## Files

- [`workflows/content-categorizer.json`](workflows/content-categorizer.json) is the main workflow.
- [`workflows/error-alert.json`](workflows/error-alert.json) is the error workflow that emails the spam articles.

## Flow

HTTP Request (POST, 7 sample articles) → Webhook → Split Out → Text Classifier (Technology / Business / Health / Entertainment / Sports) → Edit nodes add `category` + `timestamp` → Merge → Summarize (count per category)

Spam goes to the **Other** branch → Aggregate → waits for the statistic → Stop and Error lists all spam articles → the error workflow emails them.

## Setup

1. Import both workflows and select your Anthropic and Gmail credentials.
2. In the main workflow, open **Settings → Error Workflow** and select the error workflow.
3. Activate the main workflow, then paste its **production** webhook URL into the HTTP Request node.
4. Click **Execute workflow**.

Error workflows only run for production executions, so use the production URL rather than the test URL.
