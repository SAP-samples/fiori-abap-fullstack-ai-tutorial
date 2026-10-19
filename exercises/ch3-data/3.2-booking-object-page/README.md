# 3.2 Add a second object page for the bookings

## 🎯 Goal

You complete the shape of the app. The generator gave you a List Report of Travel records
and one object page for a single Travel, with the bookings shown as an inline table on that
page. In this exercise you add a second object page, one for a single Booking, and wire the
navigation so that selecting a booking row opens it as its own page. Now that you have a real
record from [3.1](../3.1-value-helps/README.md), you can navigate into it and see the new page
work. From one prompt, the MCP server for SAP Fiori adds the page and the route for you.

## ✅ Prerequisites

- A real Travel record with a Booking, created in [3.1](../3.1-value-helps/README.md), so there is something to navigate into.
- Your Fiori app still running in the preview. Keep it open. It reloads on its own after the change, so you can watch the effect there.
- A chat open in agent mode, with the MCP server for SAP Fiori available (from [0.3](../../ch0-setup/0.3-copilot-fiori-mcp/README.md)).

## 🧭 Steps

### 1. See what the generator left out

Go to the app preview in your browser. Open your Travel record to see its object page. The
bookings appear as a table section on that same page. Look at the booking row: there is no
chevron (the `>` at the end of the row) that would let you navigate into it. That missing
chevron is the tell that no object page exists for a booking, so a booking has nowhere to
show its own details or, later, its own sections. That is the gap you close now.

### 2. Ask the assistant to add the Booking object page

Send this prompt. It starts with the `/sap-fiori-app-development` skill so the assistant
follows the SAP Fiori tools conventions and uses the MCP server for SAP Fiori to do the work.
The skill already knows the app's shape, so a short request is enough.

```text
/sap-fiori-app-development In my generated SAP Fiori elements Travel app, add a second object page for the bookings.
```

### 3. Let it work

The assistant calls the MCP server for SAP Fiori to add the page and the route to the app
descriptor. Allow each tool call when VS Code asks. This is a change to the app project only,
so nothing needs to be republished on the backend.

### 4. Check the result in the running app

Go to the app preview in your browser. Once the change is applied, the preview reloads on its
own. Open your Travel record and look at the booking row again: it now has a chevron (`>`) at
the end, the sign that a detail page exists. Click the row, and instead of just editing it
inline, the app navigates to a dedicated Booking object page.

> 💡 If the preview does not update on its own, reload the browser tab manually to pull the latest app descriptor.

## 💡 What just happened

A SAP Fiori elements object page can carry sections for its navigation properties, and the
target of a to-many association can have its own object page. The generator only created the
page for the main entity, Travel. With one prompt the assistant added the second page for the
Booking and wired the route from the bookings table, so the app now has a proper drill-down:
Travel list, Travel details, Booking details. You did not edit the app descriptor by hand.

## 🔍 Verify

- The assistant reports that it added a Booking object page and wired the navigation, without changing the backend service.
- Once the preview has reloaded, the booking row on the Travel object page now shows a chevron (`>`), and clicking it opens a separate Booking object page.
- The Booking object page shows the fields of a single booking.

## ➡️ Next

The app now has both object pages, but they still show raw technical keys and unhelpful
titles. Keep the preview open. Next you hide those keys and give both pages a meaningful
header. Continue with [3.3 Hide the technical UUID keys](../3.3-hide-uuids/README.md).
