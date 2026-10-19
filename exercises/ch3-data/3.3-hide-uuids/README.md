# 3.3 Hide the technical UUID keys

## 🎯 Goal

You clean up the app so it stops showing the raw technical keys. The generator uses a
UUID, a long technical identifier, as the key of each Travel and Booking record, and
it puts that UUID in the table columns, the filter bar, and the object-page headers of
both object pages. That is not useful to a person. With one prompt you hide those
technical keys and give both object pages a meaningful header instead.

## ✅ Prerequisites

- Value helps added to your model (from [3.1](../3.1-value-helps/README.md)).
- Both object pages in place, so you can navigate to a booking and check it (from [3.2](../3.2-booking-object-page/README.md)). Keep the app running in the preview. It reloads on its own after the change, so you can watch the effect there.
- A chat open in agent mode, with the ABAP MCP server enabled and your destination and package allowlisted.

## 🧭 Steps

### 1. See the problem in the running app

Go to the app preview in your browser. In the List Report table, and in the filter
bar, you see a `UUID` column filled with long strings like
`3b8c1f2e-9a4d-4c7b-8e21-...`. Open a Travel record and look at the object page header,
it shows the same UUID as the title. Navigate into a booking to see the Booking object
page, its header shows a UUID too, and the Booking records additionally carry a
`ParentUUID`. These are the technical keys the generator exposed by default, on both
object pages.

### 2. Ask the assistant to hide the technical keys

Send this prompt. It describes what to hide and what to show instead, on both the
Travel and the Booking side, and asks the assistant to find the fields itself, so you
do not have to name any entities or positions.

```text
In my Travel and Booking metadata extensions in package ZUI_ON_ABAP on system BTP_DEV, hide the technical key fields from the UI.

- Hide the UUID field, and the ParentUUID field on the Booking entity, so they no longer appear in the list report table, the filter bar, or either object page.
- Do not hide any business fields, such as the agency, customer, dates, price, or status.
- Renumber the remaining UI positions on both entities so there are no gaps.
- Repoint the object-page headers, which currently use the UUID as the title, to meaningful fields instead:
  - Travel object page: use the description as the title and the agency as the secondary text.
  - Booking object page: use a meaningful booking field as the title, such as the flight connection or the airline, and the booking date as the secondary text.
- Activate the changed objects.

Give me a plan first, then apply it once I confirm.
```

### 3. Review the plan and confirm

Check that the plan hides `UUID` on both entities and `ParentUUID` on the Booking,
keeps every business field, and repoints both object-page headers to real fields
rather than leaving them blank. When it looks right, confirm:

```text
Looks good, apply it.
```

### 4. Let it work

The assistant edits the metadata extensions to hide the technical fields, renumbers
the remaining positions, fixes both headers, and activates the changed objects. Allow
each tool call when VS Code asks. Hiding a field is a metadata change, so the running
app reflects it on the next read, no republishing needed.

### 5. Check the result in the running app

Go to the app preview in your browser. Once the change is activated, the preview
reloads on its own. The `UUID` column is gone from the table and the filter bar, and
the Booking `ParentUUID` is gone too. Open a Travel record, the object-page header now
shows the description and agency instead of a UUID. Navigate into a booking, the
Booking object-page header now shows a meaningful title instead of a UUID. The list
and both pages finally read like trips and bookings, not like identifiers.

> 💡 If the preview does not update on its own, reload the browser tab manually to pull the latest metadata.

## 💡 What just happened

The technical keys are still there under the hood, they still identify each record,
they are just no longer shown to the user. You told the assistant which fields are
technical and which fields should title the object pages, and it updated the metadata
extensions and reactivated them. Because both object pages now exist, you could clean
them up together in the same pass. This is the kind of polish that separates a raw
generated app from one that looks intentional.

## 🔍 Verify

- The assistant reports that it hid the UUID and ParentUUID fields and activated the changed metadata extensions.
- Once the preview has reloaded, there is no UUID column in the table and no UUID in the filter bar.
- The Travel object-page header shows a meaningful title, not a UUID.
- The Booking object-page header shows a meaningful title, not a UUID.
- The business fields, agency, customer, dates, price, and status, are all still there.

## ➡️ Next

The app looks clean, but the list still has only your one record. Next you load sample
data so there is a full list to see. Continue with
[3.4 Load sample data with run classes](../3.4-sample-data/README.md).
