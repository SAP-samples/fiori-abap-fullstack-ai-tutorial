# 2.1 Connect to your system for app generation

## 🎯 Goal

You create an HTTP connection to your ABAP system in the SAP Fiori tools connection manager.
The MCP server for SAP Fiori needs this connection to download the service metadata, generate
an app, preview it, and later deploy it. You set it up once here, and every later exercise in
this chapter and beyond reuses it.

## ✅ Prerequisites

- Your RAP service published, with a working preview (from [1.3](../../ch1-abap-service/1.3-publish-service/README.md)).
- The SAP Fiori tools - Extension Pack installed (from [0.3](../../ch0-setup/0.3-copilot-fiori-mcp/README.md)).

## 🧭 Steps

The connection created by the ABAP extension in Chapter 1 and the connection used by SAP Fiori
tools are separate. So even though your system is already connected for ABAP development, you
add it once more here, this time in the SAP Fiori tools connection manager. The service binding
gives you a shortcut to do exactly that.

> 💡 The **Create a SAP Fiori App...** wizard would happily generate a whole app for you. That is not what you want here. You only walk it far enough to create and save the system connection, and then you cancel out. The app comes from a prompt in the next exercise.

### 1. Start from the service binding

Open your service binding file (the `.srvb.json` file under `ZUI_ON_ABAP` in the Explorer), the
same one you published in 1.3. Below the service name, click **Create a SAP Fiori App...**.

### 2. Select the main entity

When prompted for the entity, keep the default (**Travel**) and continue. It does not really
matter which entity you pick, because you stop before the app is generated. The wizard just
needs a selection to move on to the system connection step.

### 3. Create a new system

If your system is not yet known to SAP Fiori tools, a dialog appears saying the target system
could not be matched to a saved system. Click **Create New System**. (If you have already
created the system in a previous run, choose **Choose Saved System** instead and skip to saving.)

### 4. Fill in the system details

The **SAP System Details** form opens, mostly pre-filled from the binding:

- **System Type**: if it is not already set, choose **ABAP Environment on SAP Business Technology Platform**.
- **Connection Name**: a name is suggested from the system host. Replace it with the same
  name you use for your ABAP system, **`BTP_DEV`**. Using the same name on both sides keeps
  things simple: the prompts in the next exercises name `BTP_DEV`, and everything lines up.
- **Connection Type** and **URL**: leave these as filled in.

### 5. Test the connection

Click **Test Connection**. A browser window opens and asks you to authenticate to your system.
Sign in. When it succeeds, the form shows a confirmation that the catalog calls returned
services, for example a line like "The OData V4 catalog call returned N services." That means
SAP Fiori tools can reach your system and read its service catalog.

### 6. Save the connection, then stop

Click **Save**. The system is now stored in the SAP Fiori tools connection manager, ready for
generating, previewing, and deploying apps.

That is all you need from this wizard. You do not want to finish creating an app by hand here,
so close the wizard or cancel out of the remaining steps. The connection stays saved. You
generate the app with a prompt in the next exercise.

## 💡 What just happened

SAP Fiori tools keeps its own list of saved systems, separate from the ABAP extension. The
connection you just saved is what the MCP server for SAP Fiori uses to talk to your ABAP
system: to download the OData metadata, to run a local preview against live data, and to
deploy the finished app. Starting from **Create a SAP Fiori App...** on the binding pre-filled
most of the form for you, so all you had to do was pick the system type, authenticate, and save.

## 🔍 Verify

- The **Test Connection** step succeeded and reported that the catalog calls returned services.
- After **Save**, the system appears in your SAP Fiori tools saved systems, so you will not be
  asked to create it again.

## 📚 Further reading

- [SAP Fiori tools (documentation)](https://help.sap.com/docs/SAP_FIORI_tools)

## ➡️ Next

Your system is connected for SAP Fiori tools. Now you generate the app. Continue with
[2.2 Generate a List Report app from your Travel service](../2.2-generate-list-report/README.md).
