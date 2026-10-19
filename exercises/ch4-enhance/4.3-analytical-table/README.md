# 4.3 Add an analytical chart to the List Report

## 🎯 Goal

You add a chart to your List Report that shows total revenue grouped by travel status,
sitting above the table you already have. The table stays exactly as it is. You just
put a chart on top of it that sums up the data by status, so the page gives you a quick
visual read before you scroll the rows.

A SAP Fiori development skill does the work for you. You invoke it with the
`/sap-fiori-analytical-chart` slash command and a short line describing the chart you
want, and the skill enables aggregation on your Travel service and adds the chart above
the table.

## ✅ Prerequisites

- Your Travel service with value helps and sample data (from [3.1](../../ch3-data/3.1-value-helps/README.md) and [3.4](../../ch3-data/3.4-sample-data/README.md)). The chart needs data to show, so make sure the List Report lists some Travel records.
- Your Fiori app running in the preview (from [2.2](../../ch2-generate/2.2-generate-list-report/README.md)). Keep the preview open in your browser.
- A chat open in agent mode, with both the ABAP MCP server and the MCP server for SAP Fiori enabled, and your destination and package allowlisted (from [0.2](../../ch0-setup/0.2-vscode-adt/README.md), [0.3](../../ch0-setup/0.3-copilot-fiori-mcp/README.md), and [1.1](../../ch1-abap-service/1.1-create-package/README.md)).

## 🧭 Steps

### 1. Understand what the chart adds here

Your List Report lists one row per Travel. A chart answers a different question at a
glance: across all your Travels, how much revenue sits in each status? To answer that,
the service has to support aggregation, so it can group rows by `Status` and sum
`TotalPrice` per group. Once the service can aggregate, you add a chart that shows the
result above the table.

The measure is `TotalPrice`, aggregated as a sum. The dimension is `Status`, the same
field you gave a value help in [3.1](../../ch3-data/3.1-value-helps/README.md), so the
chart groups by New, Planned, and Booked.

### 2. Ask the assistant to add the chart

There is a SAP Fiori development skill for exactly this. You invoke it with the
`/sap-fiori-analytical-chart` slash command and add a short line describing the chart
you want. The skill takes over from there: it enables aggregation on the service and
adds the chart above the table.

```text
/sap-fiori-analytical-chart Add an analytical column chart to my Travel List Report that shows the sum of TotalPrice by Status, above the table.
```

The slash command loads the skill, and the line gives it everything it needs: the
entity (Travel), the dimension (`Status`, the field you gave a value help in
[3.1](../../ch3-data/3.1-value-helps/README.md)), the measure (`TotalPrice`), the
aggregation (sum), the chart type (column), and where the chart goes (above the table).

### 3. Let it work

The assistant enables aggregation on your Travel service, adds the chart annotation,
and wires the chart into the app. Allow each tool call when VS Code asks. The backend
change activates the projection view and its metadata extension; the app change updates
the `manifest.json`. Nothing is published again, so the app picks up the new metadata
on its next read.

> ⚠️ For aggregation to work, the service needs `@OData.applySupportedForAggregation: #FULL`
> on the projection view (the `ZC_*` view with the `TRANSACTIONAL_QUERY` contract). The
> skill adds this for you. If the app loads to a blank screen, this annotation is the
> first thing to check.

### 4. See the chart

Go to the app preview in your browser. Once the change is applied, the preview reloads
on its own and the List Report loads its data automatically, as you set it up in
[4.1](../4.1-app-behavior/README.md).

The List Report now shows a column chart of total revenue per status above the table.
Each bar is one status, and its height is the summed total price of the Travels in that
status. Selecting a bar filters the table below to that status.

> 💡 If the preview does not update on its own, reload the browser tab manually to pull
> the latest metadata and app descriptor.

## 💡 What just happened

You added a chart to your List Report without writing any CDS or editing the app by
hand. From one short prompt, the skill enabled aggregation on your Travel service,
added the chart annotation, and put the chart above the table on the List Report page.
The table itself did not change. The chart reads the same data you already loaded,
grouped and summed on the fly by the service.

## 🧠 What a skill adds on top

This chart needed two changes that fit together: aggregation on the ABAP service and a
chart in the app. You did not spell either one out. You invoked a skill, and it knew the
whole recipe.

A skill is a third kind of help, next to the change tools and the doc search you met in the
previous two exercises. Where those are single capabilities of the MCP server for SAP Fiori,
a skill is a packaged task: a set of instructions the assistant follows for one specific
goal. This one knows that an analytical chart needs aggregation enabled on the service,
which annotation to add, and how to wire the chart into the app, and in what order. You
invoke it by name with the slash command and hand it a short line of detail.

That is why the prompt was so short. The skill carries the steps, so your line only has to
supply the specifics: the entity, the dimension, the measure, and where the chart goes. For
a task you repeat or that spans the service and the app at once, a skill saves you from
spelling out every step each time.

## 🔍 Verify

- The assistant reports that it enabled aggregation on the Travel service and added the chart above the table.
- After the preview reloads, a column chart appears above the table, with one column per travel status.
- Each column's height reflects the summed total price of the Travels in that status.
- Selecting a column filters the table below to the Travels in that status.

## 🎉 That's the tutorial

Your List Report now has a chart on top of the table, and this is the last exercise in the
tutorial. Along the way you built an ABAP RAP service, generated a Fiori elements app from
it, prepared its data, and enhanced it with AI, using the ABAP MCP server and the MCP server
for SAP Fiori throughout. You also met the three ways that MCP server helps: change tools
that apply edits, a doc search that returns matching snippets, and skills that package a
whole task.

This tutorial is a living document. It will be maintained and extended over time as the
tooling grows, so check back for new exercises and updates. Thanks for working through it.

## 🚀 Keep going

You have only scratched the surface. A few ways to take it further:

- **Explore the other skills.** This tutorial used a couple of SAP Fiori development skills,
  but there are more. Type `/` in the chat to see what is available, and try one on your app.
- **Write your own prompts.** The exercises gave you tested prompts, but the real value is
  asking for what you want in your own words. Try changing a column, adding a section, or
  adjusting the app behavior, and let the assistant work with the MCP server for SAP Fiori.
- **Share feedback.** SAP Fiori tools and the MCP server are open source in the
  [SAP/open-ux-tools](https://github.com/SAP/open-ux-tools) repository. If you hit a bug,
  have an idea, or want to contribute, open an
  [issue](https://github.com/SAP/open-ux-tools/issues), start a
  [discussion](https://github.com/SAP/open-ux-tools/discussions), or read the
  [contributing guide](https://github.com/SAP/open-ux-tools/blob/main/CONTRIBUTING.md).
