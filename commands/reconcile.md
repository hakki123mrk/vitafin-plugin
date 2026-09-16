---
description: Reconcile a bank statement (pasted text or CSV) against Vitafin records
argument-hint: <account name> then paste the statement
---

Reconcile the statement the user provides against the Vitafin account: $ARGUMENTS

1. Identify the account with `list_accounts`.
2. Call `reconcile_statement` as a dry run first.
3. Report: lines matched, missing in the app, missing on the statement, and any closing
   balance difference, each as a short list.
4. Ask whether to add the missing rows. Only then call `reconcile_statement` with
   `commit: true`, and say the added rows are in the review queue.
