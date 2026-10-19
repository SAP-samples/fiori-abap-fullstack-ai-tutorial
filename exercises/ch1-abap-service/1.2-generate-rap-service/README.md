# 1.2 Generate the RAP service

## 🎯 Goal

You generate a complete transactional RAP service for a Travel and Booking data model, in one prompt, using the ABAP Cloud generator through the ABAP MCP server. When it finishes, your package holds the full backend: tables, CDS views, behavior, a service definition, and a service binding.

## ✅ Prerequisites

- The package `ZUI_ON_ABAP` created and added as a workspace folder (from [1.1](../1.1-create-package/README.md)).
- A chat open in agent mode, with the ABAP MCP server enabled and your destination allowlisted (from [0.2](../../ch0-setup/0.2-vscode-adt/README.md)).

> 💡 From here on, `ZUI_ON_ABAP` stands for the package name you chose in [1.1](../1.1-create-package/README.md). If you used a different name, substitute it wherever this tutorial shows `ZUI_ON_ABAP`.

## 🧭 Steps

### 1. Generate the service

Send this prompt. It names the generator, the package, and the data model, and lets
the generator do the rest. The Travel and Booking entities are based on the reference
structures that ship with your system.

```text
Generate a RAP UI service for travel management using the OData UI Service from Scratch generator, in package ZUI_ON_ABAP on system BTP_DEV.

Use this specification:
- Entity 1: Travel, based on the structure /DMO/TRAVEL_DATA
- Entity 2: Booking, based on the structure /DMO/BOOKING_DATA, as a child of Travel

Give me a plan first, then generate once I confirm.
```

The **OData UI Service from Scratch** generator builds a whole RAP service, including
UI annotations, from this plain description, without needing an existing table to
point at. The assistant plans the work, then calls the generator. Allow each tool call
when VS Code asks. Generation can take a moment.

### 2. Review what it created

When it finishes, the assistant reports the list of generated objects, and they are
activated for you as part of the run. For a Travel and Booking model you should see
roughly:

- Database tables for the persistent and draft data of both entities
- CDS base views (interface views) for Travel and Booking
- CDS projection views (the consumption views the service exposes)
- Metadata extensions that hold the UI annotations
- A behavior definition and a behavior implementation class
- A service definition and a service binding

The exact names are chosen by the generator and may differ from any example, so read
the list it gives you rather than assuming names. Refresh the `ZUI_ON_ABAP` folder in
the Explorer to see the objects appear under their type folders.

> ⚠️ The generator is AI-assisted, so object names and small details can vary from run to run. Always skim the generated objects before you move on, and if something looks off, ask the assistant to explain or adjust it.

## 💡 What just happened

One prompt produced an entire backend. The generator created the data model (tables and CDS views), the behavior that makes it editable with draft support, and the service definition and binding that expose it as an OData service, and it activated everything for you. This is the same RAP service you would build by hand in a much longer sitting, and it is the foundation the SAP Fiori elements app will sit on in the next chapter.

You described the model in business terms, Travel with Booking as its child, and the generator turned that into the correct set of RAP artifacts. You did not write any CDS or ABAP yourself.

## 🔍 Verify

- The assistant reports a list of generated objects covering tables, CDS views, a behavior definition and class, a service definition, and a service binding.
- Those objects show up under `ZUI_ON_ABAP` in the Explorer (refresh if needed), and none of them are flagged as inactive.
- You have noted the name of the generated service binding. You will need it when you publish the service in [1.3](../1.3-publish-service/README.md).

## 📚 Further reading

- [ABAP RESTful Application Programming Model (RAP)](https://help.sap.com/docs/abap-cloud/abap-rap/abap-restful-application-programming-model)
- [ABAP Flight Reference Scenario (SAP-samples on GitHub)](https://github.com/SAP-samples/abap-platform-refscen-flight)
- [Downloading the ABAP Flight Reference Scenario](https://help.sap.com/docs/abap-cloud/abap-rap/downloading-abap-flight-reference-scenario)

## ➡️ Next

The service exists and is active, but it is not published yet, so no UI client can reach it. In the next exercise you publish the service. Continue with [1.3 Publish the service](../1.3-publish-service/README.md).
