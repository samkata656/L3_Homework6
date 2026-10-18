# L3 Homework 2: Candidate Screening

An n8n workflow that collects job applications through a form, extracts the key details with AI, scores qualified candidates, and adds them as rows in a Google Sheet.

## Files

- [`workflows/candidate-screening.json`](workflows/candidate-screening.json) is the workflow.
- [`data/candidates_list.csv`](data/candidates_list.csv) contains the Google Sheet column headers.

## How it works

1. **Form**: name, email, phone, skills (checkboxes), work experience (free text), and expected salary.
2. **Information Extractor**: extracts the details and calculates **years of IT experience** from the text, since the form does not ask for it.
3. **If**: continues only when the candidate has at least 3 years of experience, n8n, and Ollama.
4. **Scoring (0–100)**: experience gives 5 points per year, up to 50. Skills give 10 points for core skills, 5 for relevant skills, and 2 for other skills, up to 50.
5. **Append row in sheet**: adds the candidate and the reasoning behind the score.

## Setup

1. Import `candidates_list.csv` into a new Google Sheet: **File → Import → Upload**.
2. Import the workflow, then select your Google Sheets and OpenRouter credentials.
3. In **Append row in sheet**, choose your new sheet.
4. Open the form (**Test URL**) and submit an application. The sticky note includes sample text.
