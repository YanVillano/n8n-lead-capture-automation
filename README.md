# Sales Lead Analyzer Automation

This workflow automatically analyzes incoming sales leads from **Google Forms (via Sheets)** and **Gmail**, scores them based on potential, and sends notifications to Slack channels for immediate action.

## Triggers
- **Google Sheets Trigger:** Connected to Google Forms. The workflow starts whenever the Sheet is updated with a new form submission.
- **Gmail Trigger:** Starts whenever a new email is received in the connected Gmail account.

## Nodes

### Set Fields Node
- Renames variables for readability and standardizes field names.

### Function Node (Email Extraction)
- Extracts the email **subject**, **body**, and **sender email** for further analysis.

### OpenAI Node
- Analyzes both **Google Sheets** submissions and **Gmail emails**.
- Handles both formats in a single prompt.
- Scores leads based on clarity, budget, urgency, and buying intent.

### Function Node (JSON Conversion)
- Converts the raw OpenAI output text into JSON for easy access and further processing.

### If Nodes
- **Hot Lead:** `score > 80`
- **Warm Lead:** `score >= 40 AND score <= 79`
- **Cold Lead:** `score <= 39`

### Slack Nodes
- Sends analyzed lead data to **respective Slack channels** based on lead score for immediate follow-up.

## Lead Scoring
- **Hot (80–100):** High-quality, actionable leads.
- **Warm (40–79):** Moderate-quality leads; may require additional follow-up.
- **Cold (1–39):** Low-quality or vague inquiries.

## Workflow Summary
1. Trigger fires from **Google Sheets** or **Gmail**.
2. Relevant fields are standardized.
3. Emails are parsed for subject, body, and sender info.
4. OpenAI analyzes the lead, extracts important details, and scores it.
5. JSON is parsed for structured data access.
6. If nodes route the lead to the proper Slack channel for immediate action.

