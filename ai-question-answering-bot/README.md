# AI question answering bot

An automated workflow that pulls incoming questions from a Google Sheet, answers them using Google's Gemini AI, writes the answer back to the sheet, and sends an email notification — running on a schedule with no manual steps.

## What it does

Instead of manually checking a spreadsheet for new questions and typing out replies, this workflow runs in the background, picks up unanswered rows, generates an answer using an AI agent, logs the answer back into the sheet, and emails it out automatically.

## How it works

1. **Schedule trigger** — runs the workflow automatically at a set interval.
2. **Get row(s) in sheet** — reads rows from a Google Sheet containing around 20-25 sample questions used to test the bot.
3. **If** — checks whether that row's answer column is still empty, meaning the question hasn't been answered yet. Only unanswered rows continue.
4. **Limit** — caps how many rows are processed in a single run, so the bot doesn't try to answer everything at once and hit API rate limits.
5. **AI Agent** — the core of the bot:
   - Uses **Google Gemini** as the underlying language model
   - Has a **Calculator** tool available, so it can handle questions that need actual math instead of guessing
   - Generates an answer for the question in that row
6. **Update row in sheet** (on success) — writes the AI's answer back into the spreadsheet.
7. **Send a message** — emails a notification to my own Gmail inbox once the question has been answered, confirming the run completed.
8. **Error path** — not yet connected; a planned improvement is to add a retry or alert here instead of letting failed answers disappear silently.

## Tech stack

- n8n — workflow orchestration and scheduling
- Google Sheets API — reading and writing rows
- Google Gemini API — the LLM powering the AI agent
- Gmail API — sending the answer notification

## Setup

1. Import `workflow.json` into n8n.
2. Connect your own credentials for Google Sheets, Gmail, and the Gemini API.
3. Point the **Get row(s) in sheet** node at your own sheet ID and tab.
4. Adjust the schedule interval and the **Limit** count to match your expected volume.
5. Activate the workflow.

## Possible improvements

- Wire up the **Error** output of the AI Agent with a retry or an alert email, instead of leaving failed runs unhandled.
- Add **Memory** to the AI Agent so it can reference earlier questions/answers for context.
- Add more tools beyond the calculator (e.g. a web search tool) for questions that need outside information.

## A note on workflow.json

This file is exported directly from n8n — it's the saved definition of every node and connection, not hand-written application code. The actual engineering work here was designing the workflow itself: choosing the trigger, the conditional logic that decides which rows to process, the prompt sent to the AI agent, and which tool it has access to.

## Files in this folder

- `workflow.json` — the exported n8n workflow
- `screenshot.png` — the workflow canvas, for a quick visual overview
- `README.md` — this file