# 1.3 Publish the service

## 🎯 Goal

You publish the OData service that the generator created. Publishing activates the
service endpoint so that a UI client, like the SAP Fiori elements app you build in the next
chapter, can actually reach it. The publish action sits on the service binding, but what it
does is make the service itself available. This is the last step that makes your RAP service
consumable from the outside.

## ✅ Prerequisites

- The RAP service generated and active in `ZUI_ON_ABAP` (from [1.2](../1.2-generate-rap-service/README.md)).
- The name of the generated service binding, which you noted at the end of 1.2.
- A chat open in agent mode, with the ABAP MCP server enabled and your destination allowlisted (from [0.2](../../ch0-setup/0.2-vscode-adt/README.md)).

## 🧭 Steps

### 1. Publish the service

Ask the assistant to publish the service. The publish action lives on the service binding,
so you point the assistant at the binding, and it publishes the service that binding exposes.
Replace the name in the prompt with the binding name from your own generation run, since the
generator picks the names.

```text
Publish the service exposed by the service binding <YOUR_SERVICE_BINDING> on system BTP_DEV.
```

The assistant finds the publish action on the binding and runs it. Allow the tool call when
VS Code asks. Publishing takes a few seconds.

> 💡 If you are not sure of the exact binding name, ask the assistant first: "List the service bindings in package ZUI_ON_ABAP on BTP_DEV." Then use the name it returns in the publish prompt.

> ⚠️ Sometimes the assistant claims a tool is unavailable, with a message like "The publish action tool is currently disabled in your setup, so I can't run it automatically." This is usually a false positive: the tool is enabled and works fine. The reliable workaround is to **start a new chat session** and send the publish prompt again from there. A fresh session picks the tool up correctly.

### 2. Preview the service

Now that the service is published, you can open a generated preview straight from the binding,
without any UI project yet. This is how you confirm the service really works before you build
the SAP Fiori elements app on top of it.

1. In the Explorer, under `ZUI_ON_ABAP`, expand the service bindings folder and open the
   service binding file (the `.srvb.json` file).
2. In the open binding file, look just below the service name for a row of action links:
   **Preview...**, **Create a SAP Fiori App...**, and **Test...**.
3. Click **Preview...**. VS Code opens a generated Fiori elements preview of your service in
   the browser. Select the entity when prompted to open its list page.

> 💡 If the action links do not appear above the service, close the binding file, refresh the `ZUI_ON_ABAP` folder in the Explorer, then open the binding file again. The links show up once the file reloads.

The list comes up empty, and that is expected: your service has no data yet. The preview still
proves the published service works and is reachable end to end. You load sample data into it
later in the tutorial. This preview is also generated on the fly and is not a real app. You
build the actual SAP Fiori elements app, as a project you own and extend, in the next chapter.

## 💡 What just happened

A service binding is the object that exposes your RAP service as a real, callable OData
endpoint. Until the service is published, the definitions exist but nothing outside the
system can reach them. Publishing registers the service so that OData clients can request its
metadata and data. From here on, the service has a stable URL, and the SAP Fiori elements app
in the next chapter connects straight to it.

You did the whole backend, from an empty package to a live, published OData service, without
writing code by hand. The assistant created the objects with the generator and published the
service through the ABAP MCP server.

## 🔍 Verify

- The assistant reports that the service was published successfully.
- In the Explorer, under `ZUI_ON_ABAP`, the service binding shows its service as published.
- Opening the binding file shows the **Preview...** action, and clicking it opens a working
  preview of your service in the browser (the list is empty for now, since there is no data yet).
- You still know the service binding name. You will point the SAP Fiori elements app at this
  service in the next chapter.

## ➡️ Next

Your ABAP RAP service is generated, active, and published. That completes the backend. In the
next chapter you build a SAP Fiori elements app on top of it. Continue with
[2.1 Connect to your system for app generation](../../ch2-generate/2.1-connect-system/README.md).
