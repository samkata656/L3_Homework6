# L3 Homework 1: Customer Feedback Analyzer

An n8n workflow that reads customer feedback, scores its sentiment with AI, keeps the negative comments, flags the urgent ones and emails a report.

## File

[`workflows/customer-feedback-analyzer.json`](workflows/customer-feedback-analyzer.json) contains two versions on one canvas:

- **V1 (as specified):** Data Table → Sentiment Analysis (Positive / Neutral / Negative) → add timestamp and scores → keep **negative only** → mark as URGENT when strength and confidence are both ≥ 0.85 → email report.
- **V2 (extended):** adds an Issue Classifier (Critical issue / Complaint / No issue), so a polite comment about a real problem, such as a missing order confirmation, is still caught and marked urgent.

## Setup

1. Create a Data Table named `customer_feedback` with the columns `Name` and `Feedback`.
2. Import the workflow and re-select the Data Table and the credentials (OpenRouter, Gmail).
3. Click **Execute workflow**.
