# 3.1 Add value helps for the reference data

## 🎯 Goal

You give the foreign-key fields in your Travel and Booking model a proper dropdown
(value help), so that when you create or edit a record you pick a valid agency,
customer, airline, or flight from a list instead of typing an ID blind. You do this
with one prompt to the ABAP MCP server, which finds the right reference entities on
your system and adds the value helps for you.

## ✅ Prerequisites

- Your RAP service generated and published (from [1.2](../../ch1-abap-service/1.2-generate-rap-service/README.md) and [1.3](../../ch1-abap-service/1.3-publish-service/README.md)).
- Your Fiori app generated and running in the preview (from [2.2](../../ch2-generate/2.2-generate-list-report/README.md)). Keep the preview open in your browser. It reloads on its own after each change, so you can watch the effect there.
- A chat open in agent mode, with the ABAP MCP server enabled and your destination and package allowlisted (from [0.2](../../ch0-setup/0.2-vscode-adt/README.md) and [1.1](../../ch1-abap-service/1.1-create-package/README.md)).

## 🧭 Steps

### 1. Ask the assistant to add the value helps

The generated model shows the agency, customer, airline, and flight fields as plain
input fields with no dropdown, because the generator does not add value helps on its
own. The reference data for all of these already exists on your system as part of the
Flight scenario, and that scenario ships a stable set of released value-help entities,
so you can name the exact ones to use.

Send this prompt. It names the released `/DMO/` value-help entities to use for each
field. It still asks the assistant to find your own projection views itself, since the
generated names vary from run to run.

```text
In my Travel and Booking RAP service in package ZUI_ON_ABAP on system BTP_DEV, add value helps for the reference-data fields so they show a dropdown in the app.

- First find my Travel and Booking projection views (the Z* views the generator created). Add the value helps to those projection views.
- Use these released Flight-scenario value-help entities, matching each field to the given entity and element:
  - Travel agency field -> entity /DMO/I_Agency_StdVH, element AgencyID
  - Travel customer field -> entity /DMO/I_Customer_StdVH, element CustomerID
  - Travel status field -> entity /DMO/I_Overall_Status_VH, element OverallStatus
  - Booking customer field -> entity /DMO/I_Customer_StdVH, element CustomerID
  - Booking airline/carrier field -> entity /DMO/I_Carrier_StdVH, element AirlineID
  - Booking flight/connection field -> entity /DMO/I_Connection_StdVH, element ConnectionID
- Add a @Consumption.valueHelpDefinition for each field with useForValidation: true, then activate the changed objects.
```

Because the prompt names every entity and element, there is nothing ambiguous to
clarify, so the assistant can go ahead and apply the changes directly. This is what it
adds, one value help per field:

| Entity | Field | Reference data | Released value-help entity | Element |
| --- | --- | --- | --- | --- |
| Travel | `AgencyID` | travel agencies | `/DMO/I_Agency_StdVH` | `AgencyID` |
| Travel | `CustomerID` | customers | `/DMO/I_Customer_StdVH` | `CustomerID` |
| Travel | `Status` | travel status values | `/DMO/I_Overall_Status_VH` | `OverallStatus` |
| Booking | `CustomerID` | customers | `/DMO/I_Customer_StdVH` | `CustomerID` |
| Booking | `CarrierID` | airlines | `/DMO/I_Carrier_StdVH` | `AirlineID` |
| Booking | `ConnectionID` | flight connections | `/DMO/I_Connection_StdVH` | `ConnectionID` |

### 2. Let it work

The assistant adds the value-help annotations to the projection views and activates
the changed objects. Allow each tool call when VS Code asks. Nothing is published
again, the value helps travel with the service metadata, so the running app picks
them up on its next read.

### 3. Create a Travel record using the value helps

Go back to the browser tab with your app preview. The preview reloads on its own once
the change is activated, picking up the updated service metadata.

Now put the value helps to work by adding a real record:

1. Choose **Create** to open the form for a new Travel.
2. In the agency and customer fields, open the value help and pick a value from the list instead of typing an ID. Set a begin and end date, a description, and a status from its dropdown.
3. In the Booking Items section, add a booking. Use the value helps to pick a customer, an airline, and a flight connection, then set a flight date and price.
4. Save the record.

Because the value helps also validate the input, the record saves with valid reference
IDs. You now have one real Travel with a Booking in the app.

> 💡 If the preview does not update on its own, reload the browser tab manually to pull the latest metadata.

### 4. Inspect the Travel object page

Open your new record from the list to see the Travel object page. This is your first
look at an object page with real content. The booking you added shows as a row in the
bookings table on that page. Selecting the booking row only lets you edit it inline for
now, there is no separate page for a single booking yet. You add that page next. The
page also still shows technical keys and a raw header, which you clean up shortly, but
the value helps have given you valid, populated data to work with.

## 💡 What just happened

You turned free-text foreign-key fields into guided inputs, without writing any CDS.
The assistant read your projection views, matched each foreign-key field to the
released reference entity that holds its allowed values, and added the value-help
associations for you. You then created a real Travel and Booking by picking from the
dropdowns, so the app now has valid data to work with.

## 🔍 Verify

- The assistant reports that it added value helps to the Travel and Booking projection views and activated them.
- Once the preview has reloaded, the agency, customer, and status fields on the create form show a value-help dropdown.
- The airline and flight fields on a Booking show a value-help dropdown.
- You created and saved a Travel record with a Booking by picking values from the dropdowns.
- You can open the record to see the Travel object page with your data.

## ➡️ Next

The fields are now guided and you have a real record, but the generator only made one
object page, for the Travel. A booking still has no page of its own. Next you add a
second object page for the bookings. Continue with
[3.2 Add a second object page for the bookings](../3.2-booking-object-page/README.md).
