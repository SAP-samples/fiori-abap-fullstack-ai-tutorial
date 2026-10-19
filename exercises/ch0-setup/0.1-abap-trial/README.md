# 0.1 Get an ABAP Cloud trial

## 🎯 Goal

You have a running SAP BTP ABAP Environment on a free SAP BTP trial account, and you
know its system URL. This is the ABAP system you build everything on for the rest of
the tutorial.

## ✅ Prerequisites

- A web browser.
- An email address you can receive mail at, to register for a free SAP account.

Nothing is installed on your machine yet. You do that in the next exercise.

## 🧭 Steps

### 1. Create a free SAP BTP trial account

If you already have an SAP BTP trial account, skip to step 2.

1. Open the [Get an Account on SAP BTP Trial](https://developers.sap.com/tutorials/hcp-create-trial-account.html)
   tutorial and follow it to register and log on.
2. When you reach the trial cockpit, pick a region when prompted. Your subaccount,
   organization, and space are set up for you. This takes a couple of minutes.

You end up in the [SAP BTP trial cockpit](https://cockpit.hanatrial.ondemand.com/).

### 2. Provision the ABAP Environment

The trial cockpit ships a booster that sets up an ABAP Environment instance for you,
including a developer user.

1. In the trial cockpit, open your trial subaccount.
2. Go to **Boosters** in the left navigation.
3. Search for **Prepare an Account for ABAP Trial** and choose **Start**.
4. Wait for the booster to finish. It creates the ABAP Environment service instance
   and your developer user.

> Only one ABAP trial service instance can exist at a time. If the booster reports
> that an instance already exists, you are ready and can move on.

### 3. Get the system URL

You need the system URL to connect VS Code to your ABAP system in the next exercise.

1. In the trial cockpit, open **Account Explorer** and click into your **trial**
   subaccount. The **Instances and Subscriptions** option only appears once you are
   inside the subaccount.
2. Go to **Instances and Subscriptions**.
3. On the **Instances** tab, find your **ABAP environment** instance in the list.
4. Open its **Service Keys** and choose the service key (create one if there is
   none yet).
5. In the key details, switch to the **JSON** view and copy the value of the
   **`url`** field. It looks like this:

```text
https://<guid>.abap.<region>.hana.ondemand.com
```

Keep this URL handy. You paste it into VS Code in exercise 0.2.

## 💡 What just happened

The ABAP Environment is a full ABAP system running in SAP BTP. The trial account
gives you one for free, with a developer user and the reference sample data already
loaded, so you never start from an empty database.

## 🔍 Verify

- The booster finished without errors, and the trial cockpit shows an
  **ABAP environment** instance under **Instances and Subscriptions**.
- You have the `url` value from the service key copied, in the form
  `https://<guid>.abap.<region>.hana.ondemand.com`.

You confirm the connection itself in exercise 0.2, once VS Code is connected.

## 📚 Further reading

- [Create an ABAP Environment Trial on SAP BTP](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html)

## ➡️ Next

[0.2 Install VS Code, the ABAP extension, and connect to your system](../0.2-vscode-adt/README.md)
