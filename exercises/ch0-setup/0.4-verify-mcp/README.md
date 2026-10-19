# 0.4 Check that both MCP servers respond

## 🎯 Goal

You confirm, in a single Copilot conversation, that both the ABAP MCP server and the MCP server for SAP Fiori are connected and answering. Once you see tools from both, your environment is ready for the rest of the tutorial.

## ✅ Prerequisites

- GitHub Copilot in agent mode, the SAP Fiori tools extension pack installed, and the SAP Fiori development skills in place (from [0.3](../0.3-copilot-fiori-mcp/README.md)).
- Your multi-root workspace open, with the ABAP system connected (from [0.2](../0.2-vscode-adt/README.md)). If the ABAP system node shows a yellow warning triangle, right-click it and log on again before you start.

## 🧭 Steps

### 1. Open a fresh chat in agent mode

1. Open the Chat view.
2. Make sure the mode selector is set to **Agent** and a suitable model is selected.
3. Start a new chat so the conversation is clean.

### 2. Ask the assistant to list the tools from both servers

Paste this prompt into the chat and send it:

```text
List the tools and their description for the ABAP MCP server and the MCP server for SAP Fiori in table format. Omit the MCP server prefix from tool names, group the tools semantically.
```

The assistant should return a table with tools from both servers. You will see backend tools from the ABAP MCP server (things like creating, activating, and testing RAP objects) and front-end tools from the MCP server for SAP Fiori (things like generating an app and changing its pages).

> 💡 If VS Code asks whether to allow a tool, allow it and continue. The assistant needs permission to call the MCP tools before it can read anything back.

## 💡 What just happened

This prompt is a quick smoke test. To answer it, the assistant has to reach out to both MCP servers and read back the tools they expose. If the table comes back with entries from both, it proves the whole chain works: agent mode can call tools, the ABAP MCP server is reachable through your connected system, and the MCP server for SAP Fiori is running from the SAP Fiori tools extension pack. Two servers, one conversation, which is exactly how you will work through the rest of the tutorial.

## 🔍 Verify

- The reply contains a table with tools from the ABAP MCP server (backend, RAP related).
- The same table contains tools from the MCP server for SAP Fiori (app generation and page changes).
- If either group is missing, check the matching setup step: an empty ABAP side usually means the system is not logged on ([0.2](../0.2-vscode-adt/README.md)), and a missing Fiori side usually means the SAP Fiori tools extension pack is not installed or VS Code needs a reload ([0.3](../0.3-copilot-fiori-mcp/README.md)).

> 💡 If the assistant reports that it cannot find the tools, or finds only some of them,
> right after an extension update, the MCP server is likely still running with a stale cache.
> Restart the MCP server and start a new chat session, then run the prompt again.

## 📚 Further reading

- [ABAP Development Tools for Visual Studio Code: your questions answered](https://community.sap.com/t5/technology-blog-posts-by-sap/abap-development-tools-for-visual-studio-code-your-questions-answered/ba-p/14400848) - a Q&A blog with troubleshooting tips for the ABAP extension and its MCP server, useful if a server does not respond or its tools do not show up.

## ➡️ Next

You have a working environment: an ABAP system, VS Code with both MCP servers, and the SAP Fiori development skills. In the next chapter you start building. Continue with [1.1 Create an ABAP package](../../ch1-abap-service/1.1-create-package/README.md).
