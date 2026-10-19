# 0.2 Install VS Code, the ABAP extension, and connect to your system

## 🎯 Goal

You have VS Code with the ABAP extension installed, connected to the ABAP system
from exercise 0.1. Your system shows up as a folder in a saved workspace, so you can
reopen everything later, and you can see the reference sample data.

## ✅ Prerequisites

- The system `url` from your service key, copied in [exercise 0.1](../0.1-abap-trial/README.md).

## 🧭 Steps

### 1. Install VS Code

If you already have VS Code, skip to step 2.

Download and install VS Code from
[code.visualstudio.com/Download](https://code.visualstudio.com/Download).

### 2. Install the ABAP extension

This tutorial uses the ABAP Development Tools (ADT) for VS Code extension, version
1.2.0 or later. That version also adds the MCP tools the rest of the tutorial relies on.

Install it from the Extensions view: open the Extensions view, search for
**ABAP Development Tools**, and install the extension published by **SAP SE**
(extension ID `SAPSE.adt-vscode`). Confirm the installed version is 1.2.0 or later.

### 3. Open a working folder

Create an empty folder on your machine for this tutorial, for example
`ui-on-abap`, and open it in VS Code with **File > Open Folder**. This is where
you generate the Fiori app later. Starting from a real folder also means the next
step gives you a workspace you can save and reopen.

### 4. Create a destination for your system

A destination tells the ABAP extension how to reach your system.

1. Open the Command Palette.
2. Run **ABAP: New Destination...**.
3. Choose **HTTP** as the connection type.
4. Paste the system `url` you copied in exercise 0.1:

```text
https://<guid>.abap.<region>.hana.ondemand.com
```

5. Give the destination a short name, for example:

```text
BTP_DEV
```

### 5. Add the destination to your workspace

This step activates the ABAP extension and mounts your system, so do not skip it.

1. Open the Command Palette.
2. Run **ABAP: Add Destination as Folder to the Workspace...**.
3. Select the destination you just created.
4. A browser window opens for login. Sign in there, then return to VS Code.
5. Back in VS Code, your system appears as a second folder in the Explorer,
   alongside your working folder. VS Code now has a multi-root workspace.
6. Save it with **File > Save Workspace As...** and keep it next to your working
   folder. Reopen this workspace file whenever you come back to the tutorial.

> If the ABAP system node shows a yellow warning triangle, you are not logged on.
> Right-click the node and choose **Log On to Destination...**, then sign in again
> in the browser.

### 6. Enable the ABAP MCP server and allowlist your destination

Installing the ABAP extension does not start its MCP server on its own. You turn it
on once in Settings, then tell it which destination the AI assistant is allowed to
use.

1. Open Settings (**File > Preferences > Settings**).
2. Search for `mcp`, and under the **ABAP Development** section turn on
   **Adt > Mcp Server: Enabled**. This starts a local server at
   `http://localhost:<port>/mcp` and generates a bearer token for it. The default
   port is `2236`.
3. Search for `allowlist`. Leave **Adt > Mcp Server: Allowlist Enabled** on, which
   means only the destinations you list can be reached.
4. In **Adt > Mcp Server: Allowlist**, find the **destinations** item and set its
   value to the destination name you created in step 4, for example:

```text
BTP_DEV
```

Use a comma-separated list if you have more than one destination.

> The allowlist is a safety net. It stops an AI assistant from touching any system
> except the ones you explicitly name here. If you ever see a message that a
> destination is not permitted, this setting is the place to fix it.

## 💡 What just happened

The ABAP extension connects VS Code to your ABAP system over HTTP and browses it
like a local project. Adding the destination as a folder mounts the system in the
Explorer as a second root, next to your working folder, so VS Code now holds both in
a multi-root workspace that you save and reopen any time. Turning on the ABAP MCP
server and allowlisting your destination is what lets an AI assistant read and change
ABAP objects on that system later in the tutorial.

## 🔍 Verify

- Your workspace has two folders: your working folder and your ABAP system.
- You saved the workspace file and can reopen it later.
- Open the Command Palette and type `ABAP`. You see commands such as
  **ABAP: New Destination...**, **ABAP: Open Object...**, and **ABAP: Activate**.
- In Settings, **Adt > Mcp Server: Enabled** is on, and your destination name
  appears under **Adt > Mcp Server: Allowlist** in the **destinations** item.
- Expand the system folder and open **System Library**. You can find the `/DMO/`
  packages, which hold the reference flight, travel, and booking data.

## 📚 Further reading

- [ABAP Development Tools for VS Code (Visual Studio Marketplace)](https://marketplace.visualstudio.com/items?itemName=SAPSE.adt-vscode)
- [ABAP Development Tools for VS Code (documentation)](https://help.sap.com/docs/abap-cloud/abap-development-tools-for-visual-studio-code/abap-development-tools-for-visual-studio-code)
- [ABAP Development Tools for Visual Studio Code: your questions answered](https://community.sap.com/t5/technology-blog-posts-by-sap/abap-development-tools-for-visual-studio-code-your-questions-answered/ba-p/14400848) - a Q&A blog with setup and troubleshooting tips for the extension and its MCP server.

## ➡️ Next

[0.3 Set up GitHub Copilot and the MCP server for SAP Fiori](../0.3-copilot-fiori-mcp/README.md)
