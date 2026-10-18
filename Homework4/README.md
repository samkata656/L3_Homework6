# L3 Homework 4: Meeting Notes Summariser

An n8n workflow that collects morning meeting notes from four departments (Marketing, Sales, IT and Logistics), summarises each meeting with a Map Reduce Summarization Chain, writes one summary for management, and adds a formatted date.

## File

[`workflows/meeting-notes-summariser.json`](workflows/meeting-notes-summariser.json)

## Flow

Schedule Trigger (08:00) → 4 Edit nodes with meeting notes → Merge → Code node (combines the notes into one item, separated by a divider) → Summarization Chain (Map Reduce + Character Text Splitter) → Date & Time (`dd-MM-yyyy`) → Edit node (summary + date)

## Setup

Import the workflow, select your Anthropic credentials, then click **Execute workflow**.
