# Build a Full-Stack SAP Fiori Elements App on an ABAP Service with AI

[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/fiori-abap-fullstack-ai-tutorial)](https://api.reuse.software/info/github.com/SAP-samples/fiori-abap-fullstack-ai-tutorial)

AI can carry a lot of the repetitive work in SAP development, if you let it drive
the right tools. In this tutorial you do exactly that: you talk to an AI assistant
in plain language, and it builds an ABAP service and a SAP Fiori elements app on top
of it, then helps you enhance both.

Two MCP servers do the heavy lifting: the ABAP MCP server that ships with the ABAP
extension handles the backend, and the MCP server for SAP Fiori generates and
enhances the app. That server helps in more than one way, and you meet each along the
way: change tools that apply edits, a doc search that returns matching documentation
snippets, and SAP Fiori development skills that package a whole task. You start from
the SFlight sample, build an ABAP RESTful Application Programming Model (RAP) service,
generate a List Report and Object Page, and then extend the UI and the service step by
step, all through natural-language prompts.

---

## Who this is for and what you build

This tutorial is for ABAP and full-stack developers who want to try the AI-assisted
SAP Fiori tools workflow together with the ABAP backend that feeds it, from start
to finish.

By the end you have:

- A published Travel OData service, built with AI on the SFlight sample.
- A running Fiori elements List Report and Object Page app for your Travel service.
- Value helps on the reference fields, a second object page for booking details, and
  clean object pages with the technical UUID keys hidden.
- Sample data loaded into your own tables through ABAP run classes.
- App enhancements added with AI: automatic data load, a side-by-side layout, a
  rich-text section on the object page, and an analytical chart on the List Report.

---

## How each exercise is structured

Every exercise follows the same shape, so you always know where you are:

- 🎯 **Goal:** what you have when you are done.
- ✅ **Prerequisites:** what must be true before you start.
- 🧭 **Steps:** the exact prompts and actions.
- 💡 **What just happened:** the concept behind the step.
- 🔍 **Verify:** how to confirm it worked before you move on.
- ➡️ **Next:** where to go next.

The path front-loads a one-time setup, then builds your backend service, then gives
you a running app early. From there you prepare the data and the app, and finally add
one enhancement per exercise with AI.

---

## Prerequisites

- An ABAP Cloud system you can use. A free SAP BTP ABAP Environment trial works.
  Chapter 0 walks you through getting one and importing the SFlight sample.
- VS Code on your machine.
- A GitHub Copilot subscription with chat and agent mode.
- Node.js installed, to run and preview the generated Fiori app.

Everything else, the ABAP Development Tools (ADT) for VS Code extension, SAP Fiori
tools, and the MCP server for SAP Fiori, is installed and configured in Chapter 0.

---

## Exercises

### Chapter 0: Set up your environment (once)
- [0.1 Get an ABAP Cloud trial](./exercises/ch0-setup/0.1-abap-trial/README.md)
- [0.2 Install VS Code, the ABAP extension, and connect to your system](./exercises/ch0-setup/0.2-vscode-adt/README.md)
- [0.3 Set up GitHub Copilot and the MCP server for SAP Fiori](./exercises/ch0-setup/0.3-copilot-fiori-mcp/README.md)
- [0.4 Check that both MCP servers respond](./exercises/ch0-setup/0.4-verify-mcp/README.md)

### Chapter 1: Build the ABAP service with AI
- [1.1 Create an ABAP package](./exercises/ch1-abap-service/1.1-create-package/README.md)
- [1.2 Generate the RAP service](./exercises/ch1-abap-service/1.2-generate-rap-service/README.md)
- [1.3 Publish the service](./exercises/ch1-abap-service/1.3-publish-service/README.md)

### Chapter 2: Generate your first Fiori app
- [2.1 Connect to your system for app generation](./exercises/ch2-generate/2.1-connect-system/README.md)
- [2.2 Generate a List Report app from your Travel service](./exercises/ch2-generate/2.2-generate-list-report/README.md)

### Chapter 3: Prepare the data and adjust the app
- [3.1 Add value helps for the reference data](./exercises/ch3-data/3.1-value-helps/README.md)
- [3.2 Add a second object page for the bookings](./exercises/ch3-data/3.2-booking-object-page/README.md)
- [3.3 Hide the technical UUID keys](./exercises/ch3-data/3.3-hide-uuids/README.md)
- [3.4 Load sample data with run classes](./exercises/ch3-data/3.4-sample-data/README.md)

### Chapter 4: Enhance the app with AI
- [4.1 Load data automatically and show the object page side by side](./exercises/ch4-enhance/4.1-app-behavior/README.md)
- [4.2 Add a rich-text section to the Travel object page](./exercises/ch4-enhance/4.2-rich-text-section/README.md)
- [4.3 Add an analytical chart to the List Report](./exercises/ch4-enhance/4.3-analytical-table/README.md)

---

## Working with AI in this tutorial

You use GitHub Copilot in agent mode inside VS Code. LLMs sometimes misfire or skip
a step. When that happens:

1. Pause and read the chat and terminal output before you prompt again.
2. Cancel a stuck run and start a fresh, more specific prompt.
3. Paste the exact error text from the terminal or browser console into chat and
   ask for a fix. Precise messages work far better than paraphrases.

For more on how agent mode works, see [Use agent mode in VS Code](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode).

---

## How to obtain support
[Create an issue](https://github.com/SAP-samples/fiori-abap-fullstack-ai-tutorial/issues) in this repository if you find a bug or have questions about the content.

For additional help, see [SAP Community](https://community.sap.com/).

## Contributing
If you wish to contribute code, offer fixes or improvements, please send a pull request. Due to legal reasons, contributors will be asked to accept a DCO when they create the first pull request to this project. This happens in an automated fashion during the submission process. SAP uses [the standard DCO text of the Linux Foundation](https://developercertificate.org/).

## License
Copyright (c) 2026 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSE) file.
