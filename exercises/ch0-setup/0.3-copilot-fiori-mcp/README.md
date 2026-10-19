# 0.3 Set up GitHub Copilot and the MCP server for SAP Fiori

## 🎯 Goal

By the end of this exercise you have GitHub Copilot running in agent mode, the SAP Fiori tools extension pack installed (which also brings the MCP server for SAP Fiori), and the SAP Fiori development skills copied into your workspace. That gives the AI assistant everything it needs to build and enhance the app in the later chapters.

## ✅ Prerequisites

- VS Code with the ABAP extension, connected to your system and saved as a workspace (from [0.2](../0.2-vscode-adt/README.md)).
- A GitHub account with access to GitHub Copilot. A free tier works for trying this out; check your plan at [github.com/features/copilot](https://github.com/features/copilot).
- Node.js installed. If you have used npm or npx before, you already have it. Otherwise, install the LTS version from [nodejs.org](https://nodejs.org/).

## 🧭 Steps

### 1. Install GitHub Copilot and turn on agent mode

1. Open the Extensions view in VS Code.
2. Search for **GitHub Copilot** and install it. This also installs **GitHub Copilot Chat**.
3. Sign in with your GitHub account when prompted.
4. Open the Chat view (the Chat icon in the Activity Bar, or the Chat entry in the View menu).
5. At the bottom of the Chat view, switch the mode selector to **Agent**. Agent mode is what lets Copilot call the MCP servers and act on your project, instead of only answering questions.
6. In the model picker next to the mode selector, choose a suitable model.

> 📝 The AI assistant works with many models, but they are not all equally good at driving tools and following the skills. This tutorial was tested with the latest Claude Sonnet and Claude Opus models, so if you run into odd results, switch to one of those first.

> 💡 In agent mode the assistant will start making changes on its own. When you want to see the approach before it touches anything, ask for a plan first. Something like "give me a plan first for review" makes it lay out the steps so you can check them, and only proceed once you agree.

> 💡 The first time the assistant uses a tool from one of the MCP servers, VS Code asks whether to allow it. You can allow it once, for the session, or always. Choosing to allow the MCP tools is what lets the assistant actually run them, so pick the option you are comfortable with and continue.

### 2. Install the SAP Fiori tools extension pack

The MCP server for SAP Fiori ships inside the SAP Fiori tools extension pack. Once the pack is installed, the Application Modeler exposes the MCP server to GitHub Copilot automatically, so there is nothing to wire up by hand.

1. In the Extensions view, search for **SAP Fiori tools - Extension Pack**, published by **SAP SE**.
2. Install it. This is a pack, so it pulls in several extensions at once, including the Application Modeler.
3. Reload VS Code if it asks you to.

### 3. Install the SAP Fiori development skills

The SAP Fiori development skills are short guides that the AI assistant reads when it works on the front end. They cover things like adding an analytical chart, adding a visual filter, and running the create command line tool, so the assistant follows the right steps for each. For this tutorial we install them into the workspace with the `skills` command line tool.

Open a terminal in VS Code (the Terminal menu, then New Terminal), make sure you are in your working folder, and run:

```bash
npx -y skills add https://github.com/SAP/open-ux-tools/tree/main/plugins-coding-agents/fiori/skills --skill '*' -a github-copilot --copy -y
```

What the parts mean:

- `--skill '*'` installs all available SAP Fiori development skills.
- `-a github-copilot` installs them for the GitHub Copilot agent.
- `--copy` writes plain file copies instead of symlinks, which keeps things working on Windows.

The command creates a `.agents/skills/` folder in your working folder with one subfolder per skill, plus a `skills-lock.json` file that records which versions you installed.

> 💡 Here we install the skills into the workspace, so they live next to this tutorial and travel with it. You can also install them for your user instead, so every workspace picks them up without repeating this step.

## 💡 What just happened

You gave the AI assistant three things it needs to work as a developer, not just a chatbot:

- **Agent mode** lets Copilot take actions and call tools, so it can run the MCP servers instead of only talking about them.
- The **SAP Fiori tools extension pack** brings the MCP server for SAP Fiori. That server is what generates and changes the SAP Fiori elements app. Combined with the ABAP MCP server from [0.2](../0.2-vscode-adt/README.md), the assistant can now reach both the back end and the front end from one conversation.
- The **SAP Fiori development skills** are the playbook. When you ask for a UI enhancement in a later chapter, the assistant reads the matching skill and follows its steps, so the result is correct and consistent.

## 🔍 Verify

- The Chat view shows **Agent** as the mode and a Claude Sonnet or Opus model in the picker.
- **SAP Fiori tools - Extension Pack** appears as installed in the Extensions view.
- Your working folder now contains a `.agents/skills/` folder with several skill subfolders, and a `skills-lock.json` file next to it.

## 📚 Further reading

- [SAP Fiori tools - Extension Pack (Visual Studio Marketplace)](https://marketplace.visualstudio.com/items?itemName=SAPSE.sap-ux-fiori-tools-extension-pack)
- [GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/overview)
- [First release of the MCP server for SAP Fiori (SAP Community blog)](https://community.sap.com/t5/technology-blog-posts-by-sap/sap-fiori-tools-update-first-release-of-the-sap-fiori-mcp-server-for/ba-p/14204694)
- [`@sap-ux/fiori-mcp-server` on npm](https://www.npmjs.com/package/@sap-ux/fiori-mcp-server)

## ➡️ Next

[0.4 Check that both MCP servers respond](../0.4-verify-mcp/README.md)
