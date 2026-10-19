# 4.1 Load data automatically and show the object page side by side

> **Chapter 4: Enhance the app with AI.** Your app works and has data. Now you make it
> nicer to use and richer, without leaving your editor. Each exercise in this chapter adds
> one enhancement through a short prompt, and each one shows a different way the MCP server
> for SAP Fiori helps: built-in behavior settings here, a documentation lookup next, and a
> ready-made skill in the last one.

## 🎯 Goal

SAP Fiori elements ships with behavior you can switch on without writing any code. You turn
on two of these built-in features to make the app more convenient to use:

1. The List Report starts empty and waits for you to press **Go**. You have it load the
   Travels on its own as soon as the app opens.
2. Opening a Travel replaces the whole list with the object page. You switch to a layout
   that keeps the list on the left and shows the object page next to it, side by side.

Both are settings on the app, so you make the change with one short prompt and let the MCP
server for SAP Fiori edit the app for you.

## ✅ Prerequisites

- Your Travel List Report app running in the preview (from [2.2](../../ch2-generate/2.2-generate-list-report/README.md)), with sample data loaded (from [3.4](../../ch3-data/3.4-sample-data/README.md)).
- A chat open in agent mode, with the MCP server for SAP Fiori enabled (from [0.3](../../ch0-setup/0.3-copilot-fiori-mcp/README.md)).

## 🧭 Steps

### 1. Understand what you are changing

Neither change touches your data or your ABAP service. Both are app behavior:

- **Automatic load** tells the List Report to run its query as soon as it opens, instead of
  waiting for you to press **Go**. This is a good fit here because the Travel query is
  simple and the table is small, so loading on open puts no real load on the backend. For a
  report over huge tables or an expensive query, you would leave it off and let people
  filter first.
- **Side-by-side layout** switches the app to a flexible column layout, where the list stays
  visible on the left and the object page opens in a second column on the right.

The assistant makes both edits through the MCP server for SAP Fiori, so you do not touch
the app files by hand.

### 2. Ask the assistant for both changes

Open the chat in your app project and give it this prompt.

```text
In my Travel Fiori elements app, make two changes so the app is nicer to use. Use the MCP server for SAP Fiori for both, and do not edit the files by hand.

- Load the Travel data automatically when the List Report opens, so I do not have to press Go first.
- Switch the app to a flexible column layout, so that when I open a Travel the list stays on the left and the object page shows next to it on the right.
```

The prompt names the two behaviors you want and tells the assistant to use the MCP server
for SAP Fiori, so the settings land in the right place.

### 3. Let it work

The assistant turns on the initial load for the List Report and switches the app to the
flexible column layout. Allow each edit when VS Code asks. Both are settings on the app
project only.

### 4. See the result

Go to the app preview in your browser and reload the tab. The List Report now shows the
Travels straight away, with no **Go** press needed. Click a Travel: the list stays on the
left and the object page opens beside it on the right.

> 💡 If the preview still starts empty or opens the object page full screen, reload the
> browser tab so it picks up the changed app settings.

## 💡 What just happened

You changed how the app behaves without any code. Turning on the initial load makes the
List Report fetch its data on open, which suits a list people look at every day. The
flexible column layout keeps the list in view while you work on a Travel, so you can move
between records without losing your place. Both are standard SAP Fiori elements settings,
so they keep working as the app grows.

## 🧠 How the MCP server for SAP Fiori works

This exercise is a good moment to see how the MCP server for SAP Fiori goes about a change.
Its tools follow a three-step design, and the assistant walks through them for each change
you ask for:

1. **List what is possible.** First the assistant asks the server which changes this app
   supports. The server reads your app and returns the operations it can perform, such as
   enabling the initial load or switching the layout. So the assistant only offers changes
   that actually fit your app.
2. **Get the details for one change.** Once it picks an operation, the assistant asks the
   server what that operation needs: which settings, which values, which target. The server
   returns that shape, so the assistant knows exactly what to fill in.
3. **Run the change.** With the details in hand, the assistant tells the server to apply the
   change. The server makes the edit in the right place in your app.

You saw this play out twice here, once for the initial load and once for the layout. This
is why the assistant does not hand-edit your manifest: it discovers the change, learns its
shape, and asks the server to apply it. That keeps the edits correct and in the spots SAP
Fiori elements expects, even as the tooling evolves.

These change tools are one of two ways the MCP server for SAP Fiori helps. The other is a
doc search that searches its packaged documentation for matching snippets rather than
applying edits. You use it in the next exercise.

## 🔍 Verify

- The assistant reports that it enabled the initial load and switched the app to a flexible column layout.
- After reloading the preview, the List Report shows Travels immediately, without pressing **Go**.
- Opening a Travel keeps the list on the left and shows the object page in a second column on the right.

## ➡️ Next

Your app now loads its data on open and shows records side by side. Continue with [4.2 Add a rich-text section to the Travel object page](../4.2-rich-text-section/README.md).
