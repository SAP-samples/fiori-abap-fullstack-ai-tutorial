# 3.4 Load sample data with run classes

## 🎯 Goal

You fill your Travel and Booking tables with realistic sample data, so the app shows a
real list of trips instead of an empty table. You do this by asking the assistant to
create two small ABAP console classes, one that clears the tables and one that copies
sample rows straight from the Flight scenario tables (`/dmo/travel` and `/dmo/booking`)
into yours. Because your model was built on those same reference tables, the copied data
fits and every reference ID is valid by construction. Splitting it into two classes lets
you reset and reload the data whenever you want.

## ✅ Prerequisites

- The technical keys hidden (from [3.3](../3.3-hide-uuids/README.md)).
- Your Fiori app still running in the preview. Keep it open. It reloads on its own, so the data appears there once it is loaded.
- A chat open in agent mode, with the ABAP MCP server enabled and your destination and package allowlisted.

## 🧭 Steps

### 1. Ask the assistant to create the run classes

Send this prompt. It asks for two ADT console classes and describes exactly how to
clear and populate the tables. The key idea is that it copies rows from the Flight
scenario tables your model was built on, so the data fits and every reference ID is
valid without any lookups. The prompt also spells out the details that make the classes
compile and run cleanly the first time: how to map the numeric keys to UUIDs, how to
fill the admin fields, and how to create the objects in a local package.

```text
Create two ADT console classes (if_oo_adt_classrun) in package ZUI_ON_ABAP on system BTP_DEV to manage sample data for my Travel/Booking model (a root travel table entity plus a child booking table entity, both persistent). Create and activate them, but do not run them.

- Class 1 deletes all data: delete the child booking table first, then the parent travel table, COMMIT WORK, print row counts.
- Class 2 populates data by copying sample rows from the DMO scenario tables /dmo/travel and /dmo/booking. My tables were modeled on /DMO/TRAVEL_DATA and /DMO/BOOKING_DATA, so the data payload matches and all agency, customer, carrier, connection, and flight IDs are valid by construction. Cap at 50 travels. Force every currency field to EUR. COMMIT WORK and print inserted counts.

Honor these constraints:

- Identity mapping: DMO uses numeric travel_id and booking_id keys; my model uses SYSUUID_X16 UUID keys plus a parent-UUID reference on the child. Generate a fresh UUID per travel, build a travel_id to UUID map, generate a UUID per booking, and set its parent reference from that map. Use cl_system_uuid=>create_uuid_x16_static( ).
- Fill the admin fields (created-by, created-at, last-changed-by, last-changed-at) with sy-uname and GET TIME STAMP FIELD; they are packed timestamps (timestampl), not utclong.
- Do not use ORDER BY in a FOR ALL ENTRIES select.
- ZUI_ON_ABAP is a local package (software component ZLOCAL, empty transport layer), so create the objects with an empty transport request.
- Run a syntax check and fix all errors before activating.
```

### 2. Let it work

The assistant creates the two console classes, runs a syntax check, and activates them,
but leaves running them to you. Allow each tool call when VS Code asks. Writing the data
later goes straight into your own tables, so no publishing step is involved.

### 3. Run the populate class yourself

Now you run the class that fills the tables. This is worth doing by hand once, so you
know how to execute an ABAP class and reset your data whenever you need to.

1. In the Explorer, expand your system, then **Source Code Library > Classes**, and open the populate class (Class 2, the one that inserts the records) under `ZUI_ON_ABAP`.
2. With the class open in the editor, press **F5** to run it. (You can also right-click inside the editor and choose **Run ABAP Application (Console)**. This action is only available from the open editor, not from the Explorer.)
3. The output appears in the VS Code terminal panel at the bottom, for example how many Travel and Booking records were written.

Because the class implements `if_oo_adt_classrun`, running it as an ABAP application
console executes its `main` method and prints whatever it writes to the terminal. If you
ever want to start over, run the delete class (Class 1) the same way to clear the tables,
then run the populate class again.

### 4. Check the result in the running app

Go to the app preview in your browser. Press **Go** in the List Report again to run the
query, and the table now shows a list of Travel records with agencies, customers, dates,
and prices. Open one to see its Booking records on the object page. The app is now
populated with meaningful data.

## 💡 What just happened

You now have a working app with real data, created through prompts and run by hand. The
assistant wrote the ABAP that clears your tables and copies sample rows from the Flight
scenario tables into yours, mapping the numeric keys to fresh UUIDs so parent and child
stay linked, and forcing every price to EUR. Because the copied rows come from the same
reference tables your model was built on, every agency, customer, carrier, and flight ID
is valid without a single lookup. You then ran the populate class yourself with F5 and
saw its output in the VS Code terminal, which is also how you reset the data whenever you
want. From here on, every enhancement you make to the app has real trips to show.

## 🔍 Verify

- The assistant reports that it created and activated two console classes, without running them.
- You ran the populate class with F5, and the VS Code terminal showed the inserted counts.
- After reloading the preview, the List Report shows a list of Travel records (up to fifty).
- Opening a Travel record shows its Booking records on the object page.
- The agency, customer, and other reference fields show valid values, and the value helps from [3.1](../3.1-value-helps/README.md) resolve them.

## ➡️ Next

Your app is clean and full of data. Now you start enhancing it. Continue with [4.1 Load data automatically and show the object page side by side](../../ch4-enhance/4.1-app-behavior/README.md).
