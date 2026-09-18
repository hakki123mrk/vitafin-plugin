---
description: Set Vitafin up for a new user — accounts, statements to anchor balances, cards, loans, people, recurring bills, mail capture — asking one thing at a time
argument-hint: (nothing, or what the user already has ready: "here are my statements")
---

Set the user up in Vitafin so it reflects all of their money. $ARGUMENTS

Work in this order. Check what already exists before asking, ask for **one thing at a
time**, and never invent a balance or a date.

1. **Accounts** — `list_accounts`. One account per bank account, credit card, wallet and
   broker, with the right type and currency (`create_account`). Ask for the missing ones.
2. **Statements** — for each account ask for the latest statement (PDF, CSV, screenshot or
   pasted text). Bank statements: `reconcile_statement` dry-run → commit, with the closing
   balance so the balance is anchored. Card statements: `record_card_statement`, oldest
   first, every line tagged (charge / payment / refund / fee / interest / instalment /
   conversion). If a mail connector is available in this session, search the mailbox for
   bank alerts and statements and bring them in yourself.
3. **Cards** — limit, statement day, due date (`record_card_statement` sets them from a
   statement; otherwise `set_credit_card`).
4. **Loans** — `add_loan` for everything owed or lent, with the real start date and, for
   EMIs, term and payment day.
5. **People** — `split_transaction` / `people_balances` for anyone who owes or is owed.
6. **Recurring** — `add_recurring_rule` for rent, subscriptions, EMIs, salary.
7. **Categories** — `search_transactions` with `category_id: sys.uncategorized`; propose
   categories grouped by merchant, apply with `learn_category: true`.
8. **Going forward** — tell the user to turn on mail capture in the app (Settings →
   Capture) for bank alerts, and that any statement can be forwarded to you.

Finish with `net_worth` and a short list of what is still missing.
