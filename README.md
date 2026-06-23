# n8n automation projects

A few automation workflows I've built using n8n. Most combine regular integrations like Google Sheets and Gmail with an AI agent powered by the Gemini API.

## Projects

### AI question answering bot
Watches a Google Sheet for unanswered questions, gets an AI agent (running on Gemini, with a calculator tool) to answer them, writes the answer back, and sends me an email once it's done.
[Full README here](./ai-question-answering-bot/README.md)

More projects will get added here as I document them.

## About these workflows

These are built visually in n8n's editor, not typed out as application code. The `workflow.json` file in each folder is just what n8n exports when you save a workflow. The actual work was in designing the logic itself: the trigger, the branching conditions, the prompt sent to the AI agent, and which tools it has access to. Each project's own README goes into more detail on that.