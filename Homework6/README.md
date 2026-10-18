# L3 Homework 6: Expense Receipt Assistant

An n8n system that reads expense receipts with AI, applies a company expense policy, asks a manager when needed, and reports to finance. Built by Samuil Nikolov ([samkoBuilds](https://samkobuilds.com)).

## Workflows

| File | Description |
|---|---|
| [`01-main-receipt-processing.json`](workflows/01-main-receipt-processing.json) | Gmail trigger → AI reads the receipt photo → skips duplicates → checks the policy → approves, asks the manager (Send and Wait form) or rejects → saves to `expenses` and emails the employee. |
| [`02-weekly-report.json`](workflows/02-weekly-report.json) | Every Monday 08:00: last week's totals per department and category (Summarize), an AI-written summary (Basic LLM Chain), emailed to finance. Sends a "no expenses" email for empty weeks. |
| [`03-error-alert.json`](workflows/03-error-alert.json) | Error workflow: emails an alert with the failed node, error message and a link whenever another workflow crashes. |
| [`04-expense-chat.json`](workflows/04-expense-chat.json) | Chat AI Agent that answers "How much did I spend on travel?" using the two sub-workflows below as tools, after email verification. |
| [`05-expense-lookup-subworkflow.json`](workflows/05-expense-lookup-subworkflow.json) | Tool: checks the verification code, then returns the employee's totals per category. Returns ACCESS DENIED for a wrong or expired code. |
| [`06-send-code-subworkflow.json`](workflows/06-send-code-subworkflow.json) | Tool: emails a 6-digit verification code (valid 10 minutes) to registered employees only. |

## Data tables

CSV files in [`data_tables/`](data_tables): `employees`, `expense_policy`, `expenses` (headers only) and `chat_codes` (headers only).

## Setup

1. Create the 4 Data Tables from the CSVs and check the column types: numbers as Number, `allowed` as Boolean, `receipt_date` and `expires_at` as Date, `code` as String.
2. Import the workflows, sub-workflows (05, 06) first.
3. Re-select the Data Tables, sub-workflows and credentials (Gmail, Anthropic) in each node, since IDs change on import.
4. Set **Error Workflow** to the error alert in each workflow's settings, and publish all workflows.

## Extras beyond the task

- Food expenses need a stated business purpose, otherwise they go to the manager.
- Managers can approve a partial amount.
- Old BGN receipts are converted to EUR at the fixed rate 1.95583.
- The chat uses one-time email codes, enforced inside the lookup sub-workflow rather than only in the AI prompt.

## Known limitations

- Only EUR and BGN are converted; other currencies are labelled (e.g. RON) but not converted.
- The chat shows all-time totals only, with no date filter.
