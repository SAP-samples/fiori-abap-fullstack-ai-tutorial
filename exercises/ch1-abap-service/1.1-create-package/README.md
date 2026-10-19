# 1.1 Create an ABAP package

## 🎯 Goal

You create an ABAP package on your system to hold every backend object you build in this chapter. You do it with a prompt, so this is also your first real task where the AI assistant drives the ABAP MCP server on your behalf.

## ✅ Prerequisites

- Both MCP servers responding in one conversation (from [0.4](../../ch0-setup/0.4-verify-mcp/README.md)).
- Your multi-root workspace open, with the ABAP system connected. If the system node shows a yellow warning triangle, right-click it and log on again.

## 🧭 Steps

### 1. Ask the assistant to create the package

Open a chat in agent mode and send this prompt. You can change the name and
description if you like, but keep the name starting with `Z` and 30 characters or
fewer.

```text
Create an ABAP package on system BTP_DEV with these properties:
- Name: ZUI_ON_ABAP
- Description: UI on ABAP tutorial
- Superpackage: ZLOCAL
- Software component: ZLOCAL

This is a local package under ZLOCAL, so no transport request is needed.
```

Replace `BTP_DEV` with the destination name you gave your system in [0.2](../../ch0-setup/0.2-vscode-adt/README.md) if it differs.

> 💡 Trial systems are shared, so the name `ZUI_ON_ABAP` may already be taken. If the
> assistant reports that the package already exists, pick your own name (for example
> `ZUI_ON_ABAP_01` or your initials plus a suffix), and use that same name everywhere this
> tutorial shows `ZUI_ON_ABAP`.

### 2. Let it work

The assistant calls the ABAP MCP server to create the package. Because you gave it
every required detail, it should not need to ask you anything. If VS Code asks whether
to allow a tool, allow it and continue.

### 3. See the package on your system

After the assistant reports success, expand the ABAP system folder in the Explorer
to find the new package. Local packages sit under **System Library**, so the path is:

```text
BTP_DEV > System Library > ZLOCAL > ZUI_ON_ABAP
```

`BTP_DEV` is your ABAP system folder, and `ZLOCAL` is the superpackage you asked for.
If the package does not show up right away, click the refresh icon at the top of the
Explorer next to the workspace name to update the ABAP tree.

### 4. Allowlist the package for object changes

In [0.2](../../ch0-setup/0.2-vscode-adt/README.md) you allowlisted your destination so the
assistant could reach the system. Changing objects inside a package needs one more entry:
the package itself has to be on the allowlist, or the assistant will be blocked when it
tries to generate objects into it in the next exercise.

1. Open **Settings** and search for `allowlist`.
2. Find **Adt > Mcp Server: Allowlist** and edit the **`packages-objectChanges`** item.
3. Set its value to your package name, then confirm:

```text
ZUI_ON_ABAP
```

Use a comma-separated list if you ever work in more than one package. Leave
**Adt > Mcp Server: Allowlist Enabled** on, so the allowlist stays in effect.

> 💡 If a later step fails with a "not permitted" or "access denied" style message when the assistant tries to change objects, this package allowlist entry is the first thing to check.

### 5. Add the package as its own workspace folder

Digging through hundreds of packages under **System Library** every time gets old
fast. Add your package as its own folder so it is always one click away.

1. Open the Command Palette.
2. Run **ABAP: Add Package as Folder to Workspace**.
3. Pick your system, then choose `ZUI_ON_ABAP`.

The package now shows up as a third folder in your multi-root workspace, next to your
working folder and the full ABAP system. Everything you generate in this chapter lands
here, so you can watch it fill up without scrolling. The new folder is saved to your
workspace automatically, so it is there when you reopen it.

## 💡 What just happened

You did not open a wizard or fill in a form. You described the package you wanted, and
the assistant called the ABAP MCP server to create it for you. On a trial system,
local objects live under the `ZLOCAL` superpackage with software component `ZLOCAL`
and need no transport request, which is why the prompt spells those out. This is the
pattern for the whole tutorial: you say what you want in plain language, and the
assistant uses the right tool to do it on your system.

A package is just a container. Everything you generate next, the data model, the
service, and the binding, lands inside this package. Adding it as its own workspace
folder keeps all of that work together and one click away, instead of buried in the
system tree. Allowlisting the package tells the ABAP MCP server it is allowed to make
changes there, which is what the generator does in the next exercise.

## 🔍 Verify

- The assistant reports the package was created.
- The package appears in the Explorer at **System Library > ZLOCAL > ZUI_ON_ABAP**
  under your ABAP system folder (refresh if needed).
- `ZUI_ON_ABAP` also shows up as its own folder at the top level of the Explorer,
  as a third root in the workspace.
- `ZUI_ON_ABAP` is listed in the **`packages-objectChanges`** allowlist item.
- The package name is `ZUI_ON_ABAP`, its superpackage is `ZLOCAL`, and its software
  component is `ZLOCAL`.

## ➡️ Next

[1.2 Generate the RAP service](../1.2-generate-rap-service/README.md)
