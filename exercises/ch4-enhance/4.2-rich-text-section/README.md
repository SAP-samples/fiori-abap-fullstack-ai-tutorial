# 4.2 Add a rich-text section to the Travel object page

## 🎯 Goal

You add a new section to the Travel object page that edits the `Description` field with a
rich-text editor, so people can write formatted text instead of a plain line. The editor
is a SAP Fiori elements *building block*, dropped into a custom section on the page.

You write a short prompt for this. It leans on the doc search built into the MCP server
for SAP Fiori to look up the right building-block syntax and manifest wiring, so the
result matches the current, correct approach.

## ✅ Prerequisites

- Your Travel List Report app running in the preview (from [2.2](../../ch2-generate/2.2-generate-list-report/README.md)), with a Travel object page you can open.
- Sample data loaded (from [3.4](../../ch3-data/3.4-sample-data/README.md)), so you have a Travel to open and a `Description` to edit.
- A chat open in agent mode, with the MCP server for SAP Fiori enabled (from [0.3](../../ch0-setup/0.3-copilot-fiori-mcp/README.md)).

## 🧭 Steps

### 1. Understand what you are adding

The object page already shows the `Description` as a plain field. A rich-text editor lets
you format that text: bold, lists, headings, and so on. In a SAP Fiori elements app you do
not hand-code such an editor. You add a small *fragment* that holds the RichTextEditor
building block, then register it as a custom section on the object page in the app
manifest. The app renders it, bound to the `Description` field.

This is a change on the app project, not on the ABAP service.

### 2. Ask the assistant to add the rich-text section

Open the chat in your app project and give it this prompt. It names the field and the
section you want, and it tells the assistant to confirm the building-block syntax with the
doc search first.

```text
In my Travel Fiori elements app, add a new custom section to the Travel object page that lets me edit the Description field with a rich-text editor.

- Look up how to add the RichTextEditor building block in a custom section, using the doc search of the MCP server for SAP Fiori.
- Create the fragment for the section and bind the editor to the Description field.
- Register the section on the Travel object page in the manifest, with the title "Description".
- Give every control in the fragment an id attribute, since the app has flexEnabled set and empty ids cause errors.
```

The prompt says which field to edit and where the section goes, and it leaves the exact
building-block syntax and manifest keys to the doc search.

### 3. Let it work

The assistant looks up the building block, creates a fragment with the RichTextEditor
bound to `Description`, and registers the section in the manifest. Allow each edit when VS
Code asks. This changes files in your app project only.

### 4. See the rich-text section

Go to the app preview in your browser and open a Travel. Since you switched the app to a
side-by-side layout in [4.1](../4.1-app-behavior/README.md), the object page opens next to
the list. It now has a **Description** section with a rich-text editor. To type into it,
switch the object page to edit mode first: press **Edit** at the top of the page. Now the
editor is active, so you can type and use the toolbar to make text bold or add a list, then
save.

> 💡 If the section does not appear, reload the browser tab so the preview picks up the
> manifest change.

## 💡 What just happened

You extended the object page with a building block, the same kind SAP Fiori elements uses
for its own content. The fragment holds the RichTextEditor and binds it to `Description`,
and the manifest slots that fragment in as a section on the page. Because it is a standard
building block, it behaves like the rest of the page: it respects the draft, saves with
the Travel, and needs no custom controller.

## 🧠 How the MCP server for SAP Fiori helped here

The prompt told the assistant to look the building block up with the doc search of the MCP
server for SAP Fiori, and that is worth a closer look. The doc search is a different kind of
help than the change tools from the previous exercise. It does not edit your app, and it does
not call out to the internet. The documentation ships with the MCP server package as small,
pre-processed snippets. When the assistant sends a query, the doc search matches it against
those snippets and returns a ranked list of the closest ones for the assistant to read: the
building-block name, its attributes, the binding, and how to register a custom section in
the manifest.

Those snippets come from more than one place. They cover the official SAP Fiori elements
documentation, the sample apps that ship working examples, the SAP Fiori Development Portal
with its runnable building-block demos, and the documentation of the SAP Fiori tools command
line. So the assistant sees not just the reference text but also real, working code for the
same building block.

That matters because syntax and options change over time, and a model on its own may recall
an old or made-up form. By reading current snippets first, the assistant works from the real,
up-to-date reference before it writes the fragment and the manifest entry. So the same MCP
server gives you two kinds of help: change tools to apply edits, from the previous exercise,
and doc search to return matching snippets from its packaged documentation, which you used
here. In the next exercise you use a third kind of help, a skill, which packages a whole task
into one reusable prompt.

## 🔍 Verify

- The assistant reports that it created a fragment with the RichTextEditor building block and registered a section in the manifest.
- The app builds with no errors.
- After reloading the preview and opening a Travel, the object page shows a **Description** section with a rich-text editor.
- With the object page in edit mode, you can format text in the editor and save it with the Travel.

## 📚 Further reading

- [SAP Fiori Development Portal](https://ui5.sap.com/test-resources/sap/fe/core/fpmExplorer/index.html#/topic/introduction) - the developer portal for SAP Fiori elements, with live examples you can inspect.
- [RichTextEditor building block](https://ui5.sap.com/test-resources/sap/fe/core/fpmExplorer/index.html#/buildingBlocks/rte/rteDefault) - the specific building block from this exercise, with a runnable sample and its code.

## ➡️ Next

Your object page now has a rich-text section. Continue with [4.3 Add an analytical chart to the List Report](../4.3-analytical-table/README.md).
