# Build with AI

If you're writing code with an AI assistant, you can skip the manual integration work. Connect your agent to the API Direct [MCP server](/docs/mcp-claude-code) and it can wire up endpoints for you directly.

## Why it works

The MCP server exposes every API Direct endpoint to your agent — including the exact input parameters and response structure for each one. Your assistant doesn't have to guess at the schema or read through docs page by page. It already has everything it needs to call an endpoint correctly and map the response into your code.

That means instead of integrating each endpoint by hand, you can describe what you want and let your agent do it in one shot.

## Example prompts

Once the MCP is connected, try asking your assistant things like:

- "Implement all of the TikTok endpoints in my codebase."
- "Add every Google search endpoint to my API client."
- "Create typed functions for each Reddit endpoint with proper response models."
- "Wire up the LinkedIn job search endpoint and render the results in my app."

Your agent will pull the correct parameters and response shapes from the MCP and generate the integration code for you.

## Getting started

1. Connect the MCP server in your tool of choice — [Claude Code](/docs/mcp-claude-code), [Cursor](/docs/mcp-cursor), [Claude Desktop](/docs/mcp-claude-desktop), or [ChatGPT](/docs/mcp-chatgpt).
2. Ask it to implement the endpoints you need.
3. Review the generated code and run it.

That's it — no copy-pasting schemas, no hand-writing request boilerplate.
