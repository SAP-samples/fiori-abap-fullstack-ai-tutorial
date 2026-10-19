# 2.2 Generate a List Report app from your Travel service

## 🎯 Goal

You generate a running SAP Fiori elements List Report app on top of your published Travel
service, from a single prompt. The MCP server for SAP Fiori downloads the service metadata,
scaffolds the project, and wires it to your system. This is the early win: a real app project
you own, built on your ABAP backend, in one step.

## ✅ Prerequisites

- Your system connected in the SAP Fiori tools connection manager (from [2.1](../2.1-connect-system/README.md)).
- Your Travel service published (from [1.3](../../ch1-abap-service/1.3-publish-service/README.md)).
- A chat open in agent mode, with the MCP server for SAP Fiori available (from [0.3](../../ch0-setup/0.3-copilot-fiori-mcp/README.md)).

## 🧭 Steps

### 1. Ask the assistant to generate the app

Send this prompt. It starts with the `/sap-fiori-app-development` skill so the assistant
follows the SAP Fiori tools conventions and uses the MCP server for SAP Fiori to do the work.
It names the service and the main entity, tells the assistant where to put the project, and
pins the UI5 version. Replace `<YOUR_SERVICE>` with the name of your published service, which
you noted in [1.3](../../ch1-abap-service/1.3-publish-service/README.md). If you are not sure
of the name, ask the assistant to list the services on your connected system first.

```text
/sap-fiori-app-development Generate a standalone SAP Fiori elements List Report Object Page app from my published OData service <YOUR_SERVICE> on system BTP_DEV.

- Main entity: Travel
- Store the app in the workspace root folder
- Use UI5 version 1.148.12

Give me a plan first, then generate once I confirm.
```

Replace `BTP_DEV` with your own system name if it differs.

### 2. Review the plan and confirm

Because the prompt asks for a plan first, the assistant does not generate anything yet. It
replies with a short plan: the template it will use (List Report Object Page), the service and
main entity, the target folder, and the UI5 version. Read it over and check it matches what you
asked for, in particular the service name, the `Travel` entity, and the UI5 version.

When the plan looks right, tell the assistant to go ahead, for example:

> 💡 The assistant may offer to add a second object page for the bookings right away.
> Decline it here and keep the plan to the List Report and the Travel object page only. You
> add the booking object page yourself later, in [3.2](../../ch3-data/3.2-booking-object-page/README.md),
> with a prompt that demonstrates one use of the MCP server for SAP Fiori.

```text
Looks good, generate it.
```

If something is off, say what to change instead, and the assistant adjusts the plan before
generating.

### 3. Let it work

The assistant calls the MCP server for SAP Fiori to generate the app. Allow each tool call
when VS Code asks. Generation downloads the service metadata, creates the project, and
configures the connection to your system, so it takes a moment.

> 💡 The app is created in your working folder, the folder you opened in [0.2](../../ch0-setup/0.2-vscode-adt/README.md) as the first root of your multi-root workspace. The ABAP system and your package are separate roots in the same workspace, so the frontend project and the backend objects stay side by side.

> 💡 After generating, the assistant may need to install the app's dependencies with `npm install`. You can either run `npm install` yourself in the app folder, or ask the assistant to run it for you. It downloads a large dependency tree, so it takes a few minutes the first time.

### 4. Review what it created

When the assistant reports success, a new SAP Fiori project appears in your workspace. It
holds the standard structure of a SAP Fiori elements app: a `webapp` folder with the app
descriptor (`manifest.json`), a local copy of the service metadata, and the `package.json`
with the scripts you use to run it. You did not hand-write any of it.

### 5. Preview the app

Start the preview to confirm the app runs. In the Explorer, right-click the app folder
and choose **Preview Application**. VS Code asks which preview option to run and shows a
list of the app's run scripts. Pick the first one in the dropdown, `start`. VS Code opens
the app in a browser.

The list may be empty for now, because you have not loaded any data yet. That is fine.
Seeing the app load proves the project and the connection are wired up correctly. You
load data in the next exercise.

> 💡 The preview authorizes itself against the trial system with a reentrance ticket,
> which expires after a while. When it does, the next call to the system asks you for a
> user and password. To fix it, stop the preview and start it again. This gives you a
> fresh ticket, and the app works without prompting. You keep the preview running through
> the next chapter, so you may hit this once or twice along the way.

## 💡 What just happened

From one prompt, the MCP server for SAP Fiori generated a complete List Report Object Page
app: a list of Travel records, with an object page for the details of a single record. It is
a standalone SAP Fiori project, connected to your ABAP system through the saved connection,
and it reads its shape from the OData metadata your RAP service exposes.

## 🔍 Verify

- The assistant reports that the app was generated successfully.
- A new SAP Fiori project folder appears in your workspace, with a `webapp` folder,
  a `manifest.json`, and a `package.json`.
- The `manifest.json` points at your OData service as its data source.
- The preview opens the app in a browser, even if the list is still empty.

## 📚 Further reading

- [SAP Fiori elements (SAPUI5 Demo Kit)](https://ui5.sap.com/sdk/#/topic/03265b0408e2432c9571d6b3feb6b1fd)

## ➡️ Next

The app runs, but the list is empty, the main columns show raw technical keys, and the
input fields have no dropdowns. Keep the preview open in your browser. In the next
chapter you prepare the data and adjust the app, starting with value helps. Continue
with [3.1 Add value helps for the reference data](../../ch3-data/3.1-value-helps/README.md).
