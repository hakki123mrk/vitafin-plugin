---
name: setup
description: Connect Vitafin the first time this plugin is used, or when a Vitafin tool answers that the user is not signed in.
---

# Setting up Vitafin

1. Tell the user Vitafin needs a one-time sign-in and that a browser window will open.
2. Trigger the connection: call any Vitafin tool (for example `list_accounts`). The client
   starts the OAuth flow for `https://vitafin.io/mcp`.
3. In the browser the user enters their email and receives a 6-digit code by email; they
   enter the code and press **Allow**. A new email creates a new account with a 14-day trial.
4. Call `list_accounts` again. If the user has no accounts yet, offer to create the first one
   with `create_account` (name, type, currency, opening balance).
5. Nothing else is needed. No API keys, no configuration files.

If the browser step fails, the user can sign in at https://app.vitafin.io first and then
retry; the same email and code work in both places.
