# Tool registry

| Tool | Purpose | Called by | Authentication |
|---|---|---|---|
| GitHub Trigger | Detect push commits | Ingestion workflow | n8n GitHub credential |
| GitHub Contents API | Download source/config; commit draft/approved files | Workflow HTTP Request nodes | GitHub fine-grained token |
| OpenAI Files API | Upload PDF/image binary for Responses API | Vision ingestion | OpenAI API key |
| OpenAI Responses API | Vision analysis and FSD generation | Vision/FSD agent | OpenAI API key |
| PDF.co HTML-to-PDF | Render FSD HTML to PDF | Publisher | PDF.co API key |

MCP is not required for this first implementation. Use n8n nodes and HTTPS APIs. Never store tokens in GitHub, prompts or workflow Code nodes. Store them as n8n credentials.
