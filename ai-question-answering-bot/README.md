# AI question answering bot

This bot watches a Google Sheet for questions that haven't been answered yet, gets Gemini to actually answer them, and writes the answer back into the sheet. No manual checking needed. It also sends me an email each time one gets answered, so I know it's actually running.

## What it does

I added about 20-25 sample questions to a sheet to test this. Every minute, the workflow checks for rows where the Answer column is still empty, sends those questions to an AI agent, and updates the sheet once it has a response. Then it emails me a quick confirmation with the question, the answer, and a timestamp.

## How it works

1. A schedule trigger kicks things off automatically.
2. It reads all the rows from the Google Sheet.
3. An If node checks each row. If the Answer column is empty, it goes through. Already-answered rows get skipped.
4. A Limit node caps how many rows get processed in one run, mainly so it doesn't try to answer 20 questions at once and hit API limits.
5. From there it hits the AI Agent. This is running on Gemini, and I gave it access to a Calculator tool, so it can actually do math instead of just guessing at an answer.
6. Once it generates a response, that gets written back into the same row in the sheet.
7. Last step, it sends me an email confirming the run, with the question and answer included.

One thing I haven't fixed yet: if the AI Agent errors out, that path isn't connected to anything. Right now a failure just disappears quietly instead of alerting me. That's the next thing I want to add.

## Tech stack

- n8n handles the scheduling and orchestration
- Google Sheets API reads and writes rows
- Gemini API powers the AI agent
- Gmail API sends the notification

## Setup

If you want to run this yourself:
1. Import `workflow.json` into your own n8n instance.
2. Connect your own Google Sheets, Gmail, and Gemini credentials.
3. Point the sheet nodes at your own spreadsheet ID.
4. Adjust the schedule interval and the Limit count to whatever makes sense for your use case.
5. Turn the workflow on.

## What's not done yet

- No error handling if the AI Agent fails
- No memory, so it can't reference earlier questions for context
- Only has the Calculator tool, nothing for looking things up outside the sheet

## About workflow.json

This is just what n8n exports when you save a workflow. It's not code I typed out line by line. The actual work was building this visually in n8n: picking the trigger, setting up the If/Limit logic, writing the prompt the AI agent uses, and deciding which tool it gets access to.

## Files in this folder

- `workflow.json`: the exported workflow
- `screenshot.png`: the workflow in n8n, including a successful run
- `README.md`: this file