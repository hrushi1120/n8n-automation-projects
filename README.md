# n8n automation projects

A collection of automation workflows I built using n8n, combining standard integrations (Google Sheets, Gmail) with AI agents powered by the Gemini API.

## Projects

### AI question answering bot
Monitors a Google Sheet for unanswered questions, generates answers using a Gemini-powered AI agent with calculator tool access, writes the answer back into the sheet, and sends an email notification once it's done.
[See full project README](./ai-question-answering-bot/README.md)

*(More projects will be added here as they're documented.)*

## A note on these projects

Each workflow is built visually in n8n's editor, not as hand-written application code. The `workflow.json` in each project folder is an exported definition of that workflow's nodes and logic. The engineering work was in designing the workflow itself — the trigger conditions, the branching logic, the prompts sent to each AI agent, and which tools it can call. Each project's own README explains those decisions in detail.